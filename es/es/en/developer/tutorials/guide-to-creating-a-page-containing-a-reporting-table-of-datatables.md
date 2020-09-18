---
title: Guide to creating a page containing a reporting table of DataTables
uid: en/developer/tutorials/guide-to-creating-a-page-containing-a-reporting-table-of-datatables
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Guía para crear una página que contenga una tabla de información de DataTables

En este tutorial aprenderemos a ampliar la funcionalidad del nopCommerce con una funcionalidad personalizada para el panel de administración, y a crear una página que contenga una tabla con algunos datos a modo de informe. Así que antes de comenzar con este tutorial es necesario tener algún conocimiento previo y comprensión de algunos de los temas como.

* [nopCommerce architecture](xref:en/developer/tutorials/source-code-organization).
* nopCommerce Plugin.
* nopCommerce routing.

Si no estás familiarizado con los temas anteriores, te recomendamos encarecidamente que los conozcas primero. Sin embargo, si te sientes cómodo o al menos tienes algún conocimiento básico sobre el tema anterior, entonces eres lo suficientemente bueno para continuar con este tutorial.

Por lo tanto, en este tutorial crearemos un plugin con una página que contiene la tabla que muestra la información sobre la distribución de los usuarios por país (basada en la dirección de facturación). Vamos a repasar el proceso paso a paso para crear la funcionalidad mencionada anteriormente.

## Crear un proyecto de plugin nopCommerce

Asumo que ya sabes dónde y cómo crear un proyecto de plugin de nopCommerce y configurar el proyecto según el estándar de nopCommerce. Si no lo sabes, puedes visitar el enlace [this page](xref:en/developer/plugins/how-to-write-plugin-4.30) para saber cómo crear y configurar el proyecto de plugin nopCommerce.

Si has seguido el enlace anterior para crear y configurar tu proyecto de plugin, es posible que acabes con la estructura de carpetas de esta manera.

![image1](_static/guide-to-creating-a-page-containing-a-reporting-table-of-datatables/image1.png)

Y también sabes qué tipo de archivos contiene cada una de estas carpetas/directorios. Aquí el archivo "DistOfCustBuCountryPlugin.cs" es el inherente a la clase BasePlugin. Aquí está el código básico que queremos en este archivo por el bien de este tutorial.

```cs
public class DistOfCustByCountryPlugin: BasePlugin
    {
        public DistOfCustByCountryPlugin()
        {

        }

        public override string GetConfigurationPageUrl()
        {
            return $"{_webHelper.GetStoreLocation()}Admin/DistOfCustBuCountryPlugin/Configure";
        }

        public override void Install()
        {
            //Code you want to run while installing the plugin goes here.
            base.Install();
        }

        public override void Uninstall()
        {
            //Code you want to run while Uninstalling the plugin goes here.
            base.Uninstall();
        }
    }
```

Esta clase tiene dos métodos anulados: Instalar y desinstalar de la clase BasePlugin. Si queremos hacer algo antes de instalar y desinstalar nuestro plugin pondremos ese código antes de llamar al método de instalación y desinstalación de la clase base. Por ejemplo, si nuestro plugin tiene que crear su propia tabla, entonces crearemos esa tabla antes de llamar al método de instalación desde la clase base y, de la misma manera, si los usuarios quieren desinstalar nuestro plugin, también podemos eliminar nuestra tabla de la base de datos. En este caso, es posible que queramos ejecutar código para eliminar tablas antes de llamar al método de desinstalación de la clase base.

Primero vamos a crear un modelo llamado "CustomersDistribution" dentro de la carpeta/directorio de Models.

## #Modelos/ ClientesDistribución.cs

```cs
public class CustomersDistribution : BaseNopModel
{
    /// <summary>
    /// Country based on the billing address.
    /// </summary>
    public string Country { get; set; }

    /// <summary>
    /// Number of customers from specific country.
    /// </summary>
    public int NoOfCustomers { get; set; }
}
```

Por otra parte, agreguemos el modelo de búsqueda llamado "CustomersByCountrySearchModel" dentro de la carpeta/directorio de Modelos.

```cs
public class CustomersByCountrySearchModel : BaseSearchModel
{
}
```

nopCommerce utiliza el patrón de repositorio para el acceso a los datos que es ideal para el mecanismo de inyección de dependencia. Ahora vamos a crear un servicio que obtenga los datos necesarios de la base de datos. Para el servicio crearemos una interfaz y crearemos una clase de servicio implementando esa interfaz.

## #Servicios/ ClientesPorPaís.cs

```cs
public interface ICustomersByCountry
{
    List<CustomersDistribution> GetCustomersDistributionByCountry();
}
```

Aquí sólo tenemos una descripción del método, ya que por el bien de este plugin no necesitamos ningún otro método.

## #Servicios/ ClientesByCountry.cs

```cs
public class CustomersByCountry : ICustomersByCountry
{
    private readonly IAddressService _addressService;
    private readonly ICountryService _countryService;
    private readonly ICustomerService _customerService;

    public CustomersByCountry(IAddressService addressService, 
        ICountryService countryService,
        ICustomerService customerService)
    {
        _addressService = addressService;
        _countryService = countryService;
        _customerService = customerService;
    }

    public List<CustomersDistribution> GetCustomersDistributionByCountry()
    {
        return _customerService.GetAllCustomers()
            .Where(c => c.ShippingAddressId != null)
            .Select(c => new
            {
                _countryService.GetCountryByAddress(_addressService.GetAddressById(c.ShippingAddressId ?? 0))
                    .Name,
                c.Username
            })
            .GroupBy(c => c.Username)
            .Select(cbc => new CustomersDistribution { Country = cbc.Key, NoOfCustomers = cbc.Count() }).ToList();
    }
}
```

Aquí estamos creando una clase llamada "CustomersByCountry" que es inherente a la interfaz "ICustomersByCountry". Además, estamos implementando el método que recupera los datos de la base de datos. Utilizamos este enfoque para poder utilizar técnicas de inyección de dependencia para inyectar este servicio al controlador.

Ahora vamos a crear una clase de controlador. Una buena práctica para nombrar los controladores de los plugins es como {Grupo}{Nombre}Controlador.cs. Por ejemplo, TutorialCustomersByCountryController, aquí {Tutorial}{CustomersByCountry}Controller. Pero recuerde que no es un requisito nombrar el controlador con {Grupo}{Nombre} es sólo una forma recomendada por nopCommerce para la convención de nombres, pero la parte del controlador en el es el requisito de .Net MVC.

## #Controllers/CustomersByCountryController.cs

```cs
[AuthorizeAdmin] //confirms access to the admin panel
    [Area(AreaNames.Admin)] //specifies the area containing a controller or action
    public class DistOfCustBuCountryPluginController : BasePluginController
    {
        private readonly ICustomersByCountry _service;
        public DistOfCustBuCountryPluginController(ICustomersByCountry service)
        {
            _service = service;
        }

        [HttpGet]
        public IActionResult Configure()
        {
            CustomersByCountrySearchModel customerSearchModel = new CustomersByCountrySearchModel
            {
                AvailablePageSizes = "10"
            };
            return View("~/Plugins/Tutorial.DistOfCustByCountry/Views/Configure.cshtml", customerSearchModel);
        }

        [HttpPost]
        public IActionResult GetCustomersCountByCountry()
        {
            try
            {
                return Ok(new DataTablesModel { Data = _service.GetCustomersDistributionByCountry() });
            }
            catch (Exception ex)
            {
                return BadRequest(ex);
            }
        }
    }
```

En el controlador estamos inyectando el servicio "ICustomersByCountry" que creamos previamente para obtener datos de la base de datos. Aquí hemos creado dos Acciones una de tipo "HttpGet" y otra de tipo "HttpPost". La acción "Configurar" HttpGet devuelve una vista llamada "Configure.cshtml" que aún no hemos creado. Y la acción "GetCustomersCountByCountry HttpPost" que está usando el servicio de inyección para recuperar datos y devolver los datos en el formato json. Esta acción va a ser llamada por la tabla de datos que espera respuesta como objeto DataTablesModel. Sin embargo, aquí estamos estableciendo la propiedad de los datos que son en realidad los datos que se renderizarán en la tabla.

Ahora vamos a crear una vista con DataTables donde podemos mostrar nuestros datos que luego pueden ser vistos por nuestros usuarios. Así como un archivo _ViewImports.cshtml que contiene el código para importar todas las referencias necesarias para nuestros archivos de vista.

## #Views/ Configure.cshtml

```cs
@using Nop.Web.Framework.Models.DataTables
@{
    Layout = "_ConfigurePlugin";
}

@await Html.PartialAsync("Table", new DataTablesModel
{
    Name = "customersDistributionByCountry-grid",
    UrlRead = new DataUrl("GetCustomersCountByCountry", "TutorialCustomersByCountry"),
    Paging = false,
    ColumnCollection = new List<ColumnProperty>
    {
        new ColumnProperty(nameof(CustomersDistribution.Country))
        {
            Title = "Country",
            Width = "300"
        },
        new ColumnProperty(nameof(CustomersDistribution.NoOfCustomers))
        {
            Title = "Number Of Customers",
            Width = "100"
        }
    }
})
```

## #Views/_ViewImports.cshtml

```cs
@inherits Nop.Web.Framework.Mvc.Razor.NopRazorPage<TModel>
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper *, Nop.Web.Framework

@using Microsoft.AspNetCore.Mvc.ViewFeatures
@using Nop.Web.Framework.UI
@using Nop.Web.Framework.Extensions
@using System.Text.Encodings.Web
@using Nop.Plugin.Tutorial.DistOfCustByCountry.Models
@using Nop.Web.Framework.Models.DataTables;
@using Microsoft.AspNetCore.Routing;
```

* de las Tablas de Datos. Expliquemos la propiedad que hemos establecido para la clase DataTablesModel.
* **Nombre:** Esto será establecido como un id para DataTables.
* **UrlRead:** esta es la URL de donde DataTables va a buscar los datos para renderizar en la tabla. Aquí estamos estableciendo la URL para "GetCustomersCountByCountry" Acción del Controlador "TutorialCustomersByCountry" de que estamos obteniendo datos para las DataTables.
* **Paging:** Esta propiedad es uEn "Configure.cshtml" estamos usando una vista parcial llamada "Tabla". Esta es la implementación nopCommerce de JQuery DataTables. Podemos encontrar este archivo en "Nop.Web/Areas/Admin/Views/Shared/Table.cshtml". Allí se puede ver el código para la implementación de las DataTables. Este modelo de vista toma la clase DataTablesModel para la configuración sed para habilitar o deshabilitar la paginación de las DataTables.
* **ColumnCollection:** Esta propiedad contiene la propiedad de configuración de la columna.

Hay varias otras propiedades con las que puedes jugar para entender para qué se usa cada propiedad.

Ya casi hemos terminado, pero aún no estamos completos. Si has recordado que previamente creamos un servicio Interfaz y una clase de servicio heredando esa interfaz y hemos inyectado ese servicio a nuestro controlador. Pero aún no hemos registrado ese servicio a ningún contenedor COI. nopCommerce utiliza AutoFac para la inyección de dependencia. Por lo tanto, vamos a crear una clase para registrar el servicio para la inyección de dependencia.

## #Infraestructura/ Registro de dependencia.cs

```cs
class DependencyRegistrar : IDependencyRegistrar
{
    public int Order => 1;

    public void Register(ContainerBuilder builder, ITypeFinder typeFinder, NopConfig config)
    {
        builder.RegisterType<CustomersByCountry>().As<ICustomersByCountry>().InstancePerLifetimeScope();
    }
}
```

Aquí estamos heredando de la interfaz "IDependencia-Registro" que es proporcionada por nopCommerce. Aquí necesitamos implementar un método de "Registro" y un orden de propiedades enteras. Dentro del método Register registramos todos nuestros servicios para nuestro plugin como se muestra en el código de arriba. Bajo la capucha utiliza el AutoFac para registrar nuestros servicios DependencyRegistrar es sólo la capa creada por nopCommerce que estamos utilizando para registrar nuestras dependencias.

Ahora el último paso es registrar nuestra ruta para la acción "GetCustomersCountByCountry" del controlador "TutorialCustomersByCountry". No necesitamos registrar la ruta para la Acción "Configurar" porque ya hemos registrado eso en `DistOfCustByCountryPlugin` class.

## #Infrastructure/RouteProvider

```cs
/// <summary>
/// Represents plugin route provider
/// </summary>
public class RouteProvider : IRouteProvider
{
    /// <summary>
    /// Register routes
    /// </summary>
    /// <param name="endpointRouteBuilder">Route builder</param>
    public void RegisterRoutes(IEndpointRouteBuilder endpointRouteBuilder)
    {
        //add route for the access token callback
        endpointRouteBuilder.MapControllerRoute("CustomersDistributionByCountry", "Plugins/Tutorial/CustomerDistByCountry/",
            new { controller = "TutorialCustomersByCountry", action = "GetCustomersCountByCountry" });
    }

    /// <summary>
    /// Gets a priority of route provider
    /// </summary>
    public int Priority => 0;
}
```

Para saber más sobre el enrutamiento de nopCommerce por favor visite [this page](xref:en/developer/tutorials/register-new-routes)

Ahora sólo construye tu proyecto y corre. Ingresa como usuario administrativo y ve al menú de LocalPlugins en Configuración, allí verás tu nuevo plugin creado. Instala ese plugin. Una vez completada la instalación, verás un botón de configuración en tu plugin. Si has seguido correctamente este tutorial, verás algo parecido a la salida:

![image2](_static/guide-to-creating-a-page-containing-a-reporting-table-of-datatables/image2.png)
