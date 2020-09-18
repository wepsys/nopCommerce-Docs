---
title: Plugin with data access
uid: en/developer/plugins/plugin-with-data-access
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.skoshelev
---

# Plugin with data access

En este tutorial, usaré la arquitectura del complemento nopCommerce para implementar un rastreador de vistas de productos. Antes de comenzar con el desarrollo, es muy importante que haya leído, comprendido y completado con éxito los tutoriales que se enumeran a continuación. Pasaré por alto algunas explicaciones cubiertas en los artículos anteriores, pero puede recapitular utilizando los enlaces proporcionados.

- [Tutoriales para desarrolladores](xref:en/developer/tutorials/index)
- [Actualización de una entidad existente. Cómo agregar una nueva propiedad.](Xref:en/developer/tutorials/update-existing-entity)
- [Cómo escribir un complemento para nopCommerce 4.30](xref:en/developer/plugins/how-to-write-plugin-4.30)

Comenzaremos a codificar con la capa de acceso a datos, pasaremos a la capa de servicio y finalmente terminaremos con la inyección de dependencia.

> [!NOTe]
>
> La aplicación práctica de este complemento es cuestionable, pero no pude pensar en una función que no venga con nopCommerce y que se ajuste a una publicación de tamaño razonable. Si usa este complemento en un entorno de producción, no ofrezco garantías. Siempre me interesan las historias de éxito y me alegraría saber que la publicación aportó más que un valor educativo.

## Empezando

Cree un nuevo proyecto de biblioteca de clases "Nop.Plugin.Other.ProductViewTracker".

!![plugin-with-data-access.4.30_1](_static/plugin-with-data-access.4.30/plugin-with-data-access.4.30_1.jpg)

Agregue las siguientes carpetas y el archivo `plugin.json`.

![complemento-con-acceso-a-datos.4.30_2] _estático/ complemento-con-acceso-a-datos.4.30/complemento-con-acceso-a-datos.4.30_2.jpg)

Puede ver el contenido del archivo `plugin.json` a continuación:

```JSON
{
  "Group": "Other",
  "FriendlyName": "Product view tracker",
  "SystemName": "Other.ProductViewTracker",
  "Version": "1.00",
  "SupportedVersions": [ "4.30" ],
  "Author": "nopCommerce team",
  "DisplayOrder": 1,
  "FileName": "Nop.Plugin.Other.ProductViewTracker.dll",
  "Description": "My awesome plugin"
}
```

A continuación, agregue referencias a los proyectos **Nop.Web.Framework**.  Esto será suficiente para nosotros, ya que otras dependencias, como  **Nop.Core**  y  **Nop.Data**, seconectarán automáticamente

## La capa de acceso a datos (A.K.A. Creación de nuevas entidades en nopCommerce)

Dentro del espacio de nombres "dominio" vamos a crear una clase pública denominada ProductViewTrackerRecord. Esta clase extiende BaseEntity, pero de lo contrario es un archivo muy aburrido. Algo a recordar es que no tenemos propiedades de navegación (propiedades relacionales), porque el marco Linq2DB, que usamos para trabajar con bases de datos no admite las propiedades de navegación.



```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Domain
{
    public class ProductViewTrackerRecord : BaseEntity
    {
        public int ProductId { get; set; }
        public string ProductName { get; set; }
        public int CustomerId { get; set; }
        public string IpAddress { get; set; }
        public bool IsRegistered { get; set; }
    }
}
```

**Ubicaciones de archivos**: para averiguar dónde deberían existir ciertos archivos, analice el espacio de nombres y cree el archivo en consecuencia.

La siguiente clase a crear es la clase de constructor de entidades FluentMigrator. Dentro de la clase de mapeo, mapeamos las columnas, las relaciones de la tabla y la tabla de la base de datos.

```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Data
{
    public class ProductViewTrackerRecordBuilder : NopEntityBuilder<ProductViewTrackerRecord>
    {
        /// <summary>
        /// Apply entity configuration
        /// </summary>
        /// <param name="table">Create table expression builder</param>
        public override void MapEntity(CreateTableExpressionBuilder table)
        {
            //map the primary key (not necessary if it is Id field)
            table.WithColumn(nameof(ProductViewTrackerRecord.Id)).AsInt32().PrimaryKey()
            //map the additional properties as foreign keys
            .WithColumn(nameof(ProductViewTrackerRecord.ProductId)).AsInt32().ForeignKey<Product>(onDelete: Rule.Cascade)
            .WithColumn(nameof(ProductViewTrackerRecord.CustomerId)).AsInt32().ForeignKey<Customer>(onDelete: Rule.Cascade)
            //avoiding truncation/failure
            //so we set the same max length used in the product name
            .WithColumn(nameof(ProductViewTrackerRecord.ProductName)).AsString(400)
            //not necessary if we don't specify any rules
            .WithColumn(nameof(ProductViewTrackerRecord.IpAddress)).AsString()
            .WithColumn(nameof(ProductViewTrackerRecord.IsRegistered)).AsInt32();
        }
    }
}
```

La siguiente clase importante para nosotros será la clase de migración, que crea nuestra tabla directamente en la base de datos. Puede crear tantas migraciones como desee en su complemento, lo único que necesita para realizar un seguimiento es la versión de su migración. Creamos especialmente nuestro atributo NopMigration para que sea más fácil para usted. Al indicar aquí la fecha de creación del archivo más completa y precisa, prácticamente garantiza la unicidad de su número de migración

```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Data
{
    [SkipMigrationOnUpdate]
    [NopMigration("2020/05/27 08:40:55:1687541", "Other.ProductViewTracker base schema")]
    public class SchemaMigration : AutoReversingMigration
    {
        protected IMigrationManager _migrationManager;

        public SchemaMigration(IMigrationManager migrationManager)
        {
            _migrationManager = migrationManager;
        }

        public override void Up()
        {
            _migrationManager.BuildTable<ProductViewTrackerRecord>(Create);
        }
    }
}
```

>[!NOTe]
> Preste atención al atributo **SkipMigrationOnUpdate**, su propósito se describe por el nombre. Este atributo le permite omitir las migraciones al realizar el procedimiento de actualización del complemento.

## Capa de servicio

La capa de servicio conecta la capa de acceso a datos y la capa de presentación. Dado que es de mala educación compartir cualquier tipo de responsabilidad en el código, cada capa debe estar aislada. La capa de servicio envuelve la capa de datos con lógica empresarial y la capa de presentación dependiente de la capa de servicio. Debido a que nuestra tarea es muy pequeña, nuestra capa de servicio no hace más que comunicarse con el repositorio (el repositorio en nopCommerce actúa como una fachada al contexto del objeto).

```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Services
{
    public interface IProductViewTrackerService
    {
        /// <summary>
        /// Logs the specified record.
        /// </summary>
        /// <param name="record">The record.</param>
        void Log(ProductViewTrackerRecord record);
    }
}

namespace Nop.Plugin.Other.ProductViewTracker.Services
{
    public class ProductViewTrackerService : IProductViewTrackerService
    {
        private readonly IRepository<ProductViewTrackerRecord> _productViewTrackerRecordRepository;
        public ProductViewTrackerService(IRepository<ProductViewTrackerRecord> productViewTrackerRecordRepository)
        {
            _productViewTrackerRecordRepository = productViewTrackerRecordRepository;
        }

        /// <summary>
        /// Logs the specified record.
        /// </summary>
        /// <param name="record">The record.</param>
        public virtual void Log(ProductViewTrackerRecord record)
        {
            if (record == null)
                throw new ArgumentNullException(nameof(record));
            _productViewTrackerRecordRepository.Insert(record);
        }
    }
}
```

## Inyección de dependencia

Martin Fowler ha escrito una gran descripción de la inyección de dependencia o Inversión de control. No voy a duplicar su trabajo, y puedes encontrar su artículo [aquí](https://martinfowler.com/articles/injection.html). La inyección de dependencias gestiona el ciclo de vida de los objetos y proporciona instancias para que las utilicen los objetos dependientes. Primero, necesitamos configurar el contenedor de dependencias para que comprenda qué objetos controlará y qué reglas podrían aplicarse a la creación de esos objetos.

```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Infrastructure
{
    /// <summary>
    /// Dependency registrar
    /// </summary>
    public class DependencyRegistrar : IDependencyRegistrar
    {
        /// <summary>
        /// Register services and interfaces
        /// </summary>
        /// <param name="builder">Container builder</param>
        /// <param name="typeFinder">Type finder</param>
        /// <param name="config">Config</param>
        public virtual void Register(ContainerBuilder builder, ITypeFinder typeFinder, NopConfig config)
        {
            builder.RegisterType<ProductViewTrackerService>().As<IProductViewTrackerService>().InstancePerLifetimeScope();
        }

        /// <summary>
        /// Order of this dependency registrar implementation
        /// </summary>
        public int Order => 1;
    }
}
```

En el código anterior registramos diferentes tipos de objetos para que más tarde se puedan insertar en controladores, servicios y repositorios. Ahora que hemos cubierto los nuevos temas voy a traer de vuelta algunos de los más antiguos para que podamos terminar el plugin.



## The view component

Let's create a view component:

```csharp
namespace Nop.Plugin.Other.ProductViewTracker.Components
{
    [ViewComponent(Name = "ProductViewTracker")]
    public class ProductViewTrackerViewComponent : NopViewComponent
    {
        private readonly ICustomerService _customerService;
        private readonly IProductService _productService;
        private readonly IProductViewTrackerService _productViewTrackerService;
        private readonly IWorkContext _workContext;

        public ProductViewTrackerViewComponent(ICustomerService customerService,
            IProductService productService,
            IProductViewTrackerService productViewTrackerService,
            IWorkContext workContext)
        {
            _customerService = customerService;
            _productService = productService;
            _productViewTrackerService = productViewTrackerService;
            _workContext = workContext;
        }

        public IViewComponentResult Invoke(string widgetZone, object additionalData)
        {
            if (!(additionalData is ProductDetailsModel model))
                return Content("");

            //Read from the product service
            var productById = _productService.GetProductById(model.Id);
            //If the product exists we will log it
            if (productById != null)
            {
                //Setup the product to save
                var record = new ProductViewTrackerRecord
                {
                    ProductId = model.Id,
                    ProductName = productById.Name,
                    CustomerId = _workContext.CurrentCustomer.Id,
                    IpAddress = _workContext.CurrentCustomer.LastIpAddress,
                    IsRegistered = _customerService.IsRegistered(_workContext.CurrentCustomer)
                };
                //Map the values we're interested in to our new entity
                _productViewTrackerService.Log(record);
            }

            return Content("");
        }
    }
}
```

## The main plugin class

> [!IMPORTANT]
>
> Implementamos nuestro complemento como un widget. En este caso no necesitaremos editar un cshtml file.

```csharp
namespace Nop.Plugin.Other.ProductViewTracker
{
    public class ProductViewTrackerPlugin : BasePlugin, IWidgetPlugin
    {
        /// <summary>
        /// Gets a value indicating whether to hide this plugin on the widget list page in the admin area
        /// </summary>
        public bool HideInWidgetList => true;

        /// <summary>
        /// Gets a name of a view component for displaying widget
        /// </summary>
        /// <param name="widgetZone">Name of the widget zone</param>
        /// <returns>View component name</returns>
        public string GetWidgetViewComponentName(string widgetZone)
        {
            return "ProductViewTracker";
        }

        /// <summary>
        /// Gets widget zones where this widget should be rendered
        /// </summary>
        /// <returns>Widget zones</returns>
        public IList<string> GetWidgetZones()
        {
            return new List<string>{ PublicWidgetZones.ProductDetailsTop };
        }
    }
}
```
