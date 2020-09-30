---
title: How to write a Tax Plugin for nopCommerce 4.20
uid: en/developer/plugins/how-to-write-tax-plugin-4.20
author: git.nopsg
contributors: git.nopsg, git.DmitriyKulagin
---

# Cómo escribir un complemento de impuestos para nopCommerce

Para ampliar la funcionalidad de nopCommerce, se utilizan complementos. Hay varios tipos de complementos como "PickupInStore" y "PayPal Standard" que ya están incluidos en la distribución nopCommerce. También puede buscar varios complementos en el [sitio oficial de nopCommerce](https://www.nopcommerce.com/marketplace) para ver si alguien ya ha creado un complemento que se adapte a sus necesidades. Si no ha encontrado uno, entonces está en el lugar correcto porque este artículo lo guiará a través del proceso de creación del complemento, especialmente el complemento de impuestos, de acuerdo con sus necesidades.

## La estructura del complemento, los archivos requeridos y las ubicaciones

1. Empiece por crear un nuevo proyecto "Biblioteca de clases" en la solución. Se recomienda colocar su complemento en el directorio **Complementos**, ubicado en la carpeta raíz de la fuente, donde ya se encuentran otros complementos y widgets.

    ![image1](_static/how-to-write-a-tax-plugin-4.20/image1.png)

    > [!NOTE]
    > No confunda este directorio con el que existe en el directorio `Presentation\Nop.Web`. El directorio de complementos en el directorio Nop.Web contiene los archivos compilados de complementos.

    Un nombre recomendado para un proyecto de complemento es `Nop.Plugin. {Group}. {Name}`. `{Group}` es su grupo de complementos (por ejemplo, `Pago` o `Envío`). `{Name}` es el nombre de su complemento (por ejemplo, `FixedOrByCountryStateZip`). Por ejemplo, el complemento de impuestos `FixedOrByCountryStateZip` tiene el siguiente nombre: `Plugin.Tax.FixedOrByCountryStateZip`. Pero tenga en cuenta que no es un requisito. Y puede elegir cualquier nombre para un complemento. Por ejemplo, `MyFirstTaxPlugin`. La estructura del directorio de complementos de una solución se parece a la siguiente.

    ![image2](_static/how-to-write-a-tax-plugin-4.20/image2.png)

1. Una vez creado el proyecto del complemento, el contenido del archivo **.Csproj** debe actualizarse utilizando cualquier aplicación de edición de texto disponible. Reemplace el contenido con el siguiente:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netcoreapp2.2</TargetFramework>
            <Copyright>SOME_COPYRIGHT</Copyright>
            <Company>YOUR_COMPANY</Company>
            <Authors>SOME_AUTHORS</Authors>
            <PackageLicenseUrl>PACKAGE_LICENSE_URL</PackageLicenseUrl>
            <PackageProjectUrl>PACKAGE_PROJECT_URL</PackageProjectUrl>
            <RepositoryUrl>REPOSITORY_URL</RepositoryUrl>
            <RepositoryType>Git</RepositoryType>
            <OutputPath>..\..\Presentation\Nop.Web\Plugins\PLUGIN_OUTPUT_DIRECTORY</OutputPath>
            <OutDir>$(OutputPath)</OutDir>
            <!--Establezca este parámetro en verdadero para copiar los dlls de la "caché NuGet" a la "output" de su proyecto. Debe establecer este parámetro en verdadero si su complemento tiene un paquete nuget para asegurarse de que las dlls se copien del caché de NuGet a la output de su proyecto-->
            <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
        </PropertyGroup>
        <ItemGroup>
            <ProjectReference Include="..\..\Presentation\Nop.Web.Framework\Nop.Web.Framework.csproj" />
            <ClearPluginAssemblies Include="$(MSBuildProjectDirectory)\..\..\Build\ClearPluginAssemblies.sproj" />
        </ItemGroup>
        <!-- Este objetivo se ejecuta después del objetivo "Construir" -->
        <Target Name="NopTarget" AfterTargets="Build">
            <!-- Eliminar bibliotecas innecesarias de la ruta de los complementos-->
            <MSBuild Projects="@(ClearPluginAssemblies)" Properties="PluginPath=$(MSBuildProjectDirectory)\ $    (OutDir)" Targets="NopClear" />
        </Target>
    </Project>
    ```

    > [!NOTE]
     > El **PLUGIN_OUTPUT_DIRECTORY** debe reemplazarse por el nombre del complemento, por ejemplo, `Tax.FixedOrByCountryStateZip`.

1. Después de actualizar el archivo **.Csproj**, se debe agregar el archivo `plugin.json`, que es necesario para el complemento. Este archivo contiene metainformación que describe su complemento. Simplemente copie este archivo de cualquier otro complemento/widget existente y modifíquelo según sus necesidades. Por ejemplo, el complemento **FixedOrByCountryStateZip** tiene el siguiente archivo `plugin.json`:

    ```json
    {
        "Group": "Tax Providers",
        "FriendlyName": "Manual (Fixed or By Country/State/Zip)",
        "SystemName": "Tax. FixedOrByCountryStateZip",
        "Version": "1.29",
        "SupportedVersions": [ "4.20" ],
        "Author": "nopCommerce team ",
        "DisplayOrder": 1,
        "FileName": "Nop.Plugin.Tax. FixedOrByCountryStateZip.dll",
        "Description": "This plugin allow to configure fix tax rates or tax rates by countries, states and zip codes "
    }
    ```

    En realidad, todos los campos son autodescriptivos, pero aquí hay algunas notas. El campo **SystemName** debe ser único. El campo **Versión** es un número de versión de su complemento; puede configurarlo en cualquier valor que desee. El campo **SupportedVersions** puede contener una lista de versiones de nopCommerce compatibles separadas por comas (asegúrese de que la versión actual de nopCommerce esté incluida en esta lista, de lo contrario, no se cargará). El campo **FileName** tiene el siguiente formato **Nop.Plugin.{Group}{Name} .dll** (es el nombre del archivo de ensamblaje de su complemento). Asegúrese de que la propiedad `Copiar al directorio de salida` de este archivo esté establecida en`Copiar si es más reciente`.

    ![image3](_static/how-to-write-a-tax-plugin-4.20/image3.png)

1. El último paso requerido es crear una clase que implemente `BasePlugin` (espacio de nombres` Nop.Core.Plugins`) y la interfaz `ITaxProvider` (espacio de nombres` Nop.Services.Tax`). **ITaxProvider** implementa el método `GetTaxRate` que devuelve el tipo **CalculateTaxResult** (contiene la tasa de impuestos, los errores si los hay y el estado de éxito booleano) basado en la lógica personalizada, generalmente basada en la dirección del cliente.

## Manejo de solicitudes. Controladores, modelos y vistas

Ahora puede ver el plugin yendo a **Admin area** → **Configuration** → **Local Plugins**.

![image4](_static/how-to-write-a-tax-plugin-4.20/image4.png)

Cuando un plug
en/widget está instalado, verá el botón **Desinstalar**. Es una buena práctica desinstalar complementos/widgets que no son necesarios para mejorar el rendimiento.

![image5](_static/how-to-write-a-tax-plugin-4.20/image5.png)

Habrá el botón **Instalar** y **Eliminar** cuando un complemento / widget no esté instalado o desinstalado. 

>[!NOTE]
> La eliminación eliminará los archivos físicos del servidor.

Pero como adivinó, nuestro complemento no hace nada. Ni siquiera tiene una interfaz de usuario para su configuración. Creemos una página para configurar el complemento.

Lo que tenemos que hacer ahora es crear un controlador, un modelo, una vista y un componente de vista.

* Los controladores MVC son responsables de responder a las solicitudes realizadas en un sitio web `ASP.NET MVC`. Cada solicitud del navegador se asigna a un controlador en particular.
* Una vista contiene el marcado HTML y el contenido que se envía al navegador. Una vista es el equivalente a una página cuando se trabaja con una aplicación `ASP.NET MVC`.
* Un componente de vista que implementa **NopViewComponent** que contiene lógica y códigos para representar una vista.
* Un modelo MVC contiene toda la lógica de su aplicación que no está contenida en una vista o un controlador.

Así que comencemos:

* **Crea el modelo**. Agregue un "Modelos".
* **Crea la vista**. Agregue una carpeta `Views` en el nuevo complemento y luego agregue un archivo `.cshtml` llamado `Configure.cshtml`. Establecer la propiedad **Acción de compilación** del archivo de vista se establece en **Contenido**, y la propiedad **Copiar en el directorio de salida**se establece en **Copiar siempre**. Tenga en cuenta que la página de configuración debe usar el diseño *_ConfigurePlugin*.

```html
@model Nop.Plugin.Tax.FixedOrByCountryStateZip.Models.ConfigurationModel

@{
    Layout = "_ConfigurePlugin";
}

<div class="form-group">
    <div class="col-md-12">
        <div class="onoffswitch">
            <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="advanced-settings-mode" checked="@Model.CountryStateZipEnabled">
            <label class="onoffswitch-label" for="advanced-settings-mode">
                <span class="onoffswitch-inner"
                      data-locale-basic="@T("Plugins.Tax.FixedOrByCountryStateZip.Fixed")"
                      data-locale-advanced="@T("Plugins.Tax.FixedOrByCountryStateZip.TaxByCountryStateZip")"></span>
                <span class="onoffswitch-switch"></span>
            </label>
        </div>
    </div>
</div>
<script>
    function checkAdvancedSettingsMode(advanced) {
        if (advanced) {
            $("body").addClass("advanced-settings-mode");
            $("body").removeClass("basic-settings-mode");
        } else {
            $("body").removeClass("advanced-settings-mode");
            $("body").addClass("basic-settings-mode");
        }
    }
    checkAdvancedSettingsMode($("#advanced-settings-mode").is(':checked'));
    $(document).ready(function() {
        $("#advanced-settings-mode").click(function() {
            checkAdvancedSettingsMode($(this).is(':checked'));
            $.ajax({
                cache: false,
                url: "@Url.Action("SaveMode", "FixedOrByCountryStateZip")",
                type: "POST",
                data: {
                    value: $(this).is(':checked')
                },
                dataType: "json",
                error: function (jqXHR, textStatus, errorThrown) {
                    $("#saveModeAlert").click();
                }
            });
            ensureDataTablesRendered();
        });
    });
</script>
<nop-alert asp-alert-id="saveModeAlert" asp-alert-message="@T("Admin.Common.Alert.Save.Error")" />

@await Html.PartialAsync("~/Plugins/Tax.FixedOrByCountryStateZip/Views/_FixedRate.cshtml")
@await Html.PartialAsync("~/Plugins/Tax.FixedOrByCountryStateZip/Views/_CountryStateZip.cshtml", Model)
```

* Also make sure that you have **_ViewImports.cshtml** file into your `Views` directory. You can just copy it from any other existing plugin or widget.

![image6](_static/how-to-write-a-tax-plugin-4.20/image6.png)

 **Crea el controlador**. Agregue una carpeta `Controllers` en el nuevo complemento y luego agregue una nueva clase de controlador. Una buena práctica es nombrar los controladores de complementos **{Grupo} {Nombre} Controller.cs**. Por ejemplo, `FixedOrByCountryStateZipController`. Por supuesto, no es un requisito nombrar a los controladores de esta manera (sino solo una recomendación). Luego, cree un método de acción apropiado para la página de configuración (en el área de administración). Vamos a llamarlo `Configurar`. Prepare una clase de modelo y páselo a la siguiente vista usando una ruta de vista física: **~/Plugins / {PluginOutputDirectory} /Views/Configure.cshtml**.

```cs
public IActionResult Configure()
{
    if (!_permissionService.Authorize(StandardPermissionProvider.ManageTaxSettings))
        return AccessDeniedView();

    var taxCategories = _taxCategoryService.GetAllTaxCategories();
    if (!taxCategories.Any())
        return Content("No tax categories can be loaded");

    var model = new ConfigurationModel { CountryStateZipEnabled = _countryStateZipSettings.CountryStateZipEnabled };
    //stores
    model.AvailableStores.Add(new SelectListItem { Text = "*", Value = "0" });
    var stores = _storeService.GetAllStores();
    foreach (var s in stores)
        model.AvailableStores.Add(new SelectListItem { Text = s.Name, Value = s.Id.ToString() });
    //tax categories
    foreach (var tc in taxCategories)
        model.AvailableTaxCategories.Add(new SelectListItem { Text = tc.Name, Value = tc.Id.ToString() });
    //countries
    var countries = _countryService.GetAllCountries(showHidden: true);
    foreach (var c in countries)
        model.AvailableCountries.Add(new SelectListItem { Text = c.Name, Value = c.Id.ToString() });
    //states
    model.AvailableStates.Add(new SelectListItem { Text = "*", Value = "0" });
    var defaultCountry = countries.FirstOrDefault();
    if (defaultCountry != null)
    {
        var states = _stateProvinceService.GetStateProvincesByCountryId(defaultCountry.Id);
        foreach (var s in states)
            model.AvailableStates.Add(new SelectListItem { Text = s.Name, Value = s.Id.ToString() });
    }

    return View("~/Plugins/Tax.FixedOrByCountryStateZip/Views/Configure.cshtml", model);
}
```

* Utilice los siguientes atributos para su método de acción:

```cs
[AuthorizeAdmin] //confirma el acceso al panel de administración
[Area(AreaNames.Admin)] //especifica el área que contiene un controlador o acción
[AdminAntiForgery] //Ayuda a evitar que los scripts maliciosos envíen solicitudes de página falsificadas.
```

Por ejemplo, abra el complemento `FixedOrByCountryStateZip` y observe su implementación de`FixedOrByCountryStateZipController`.
Luego, para cada complemento que tenga una página de configuración, debe especificar una URL de configuración. La clase base llamada `BasePlugin` tiene el método `GetConfigurationPageUrl` que devuelve una URL de configuración:

```cs
public override string GetConfigurationPageUrl()
{
    return $"{_webHelper.GetStoreLocation()}Admin/{CONTROLLER_NAME}/{ACTION_NAME}";
}
```

Where *{CONTROLLER_NAME}* is a name of your controller and *{ACTION_NAME}* is a name of action (usually it's `Configure`).

Para asignar diferentes tipos impositivos según la dirección del cliente, se requiere una nueva tabla que registre todos los datos relacionados con los impuestos. Para este propósito, se agrega la carpeta `Domain` donde agregamos una clase que extiende la clase **BaseEntity**. En este caso, TaxRate.cs

![image7](_static/how-to-write-a-tax-plugin-4.20/image7.png)

Donde *{CONTROLLER_NAME}* es el nombre de su controlador y *{ACTION_NAME}* es el nombre de la acción (generalmente es `Configure`).

```cs
public override void Configure(EntityTypeBuilder<TaxRate> builder)
{
    builder.ToTable(nameof(TaxRate));
    builder.HasKey(rate => rate.Id);

    builder.Property(rate => rate.Percentage).HasColumnType("decimal(18, 4)");
}
```

\La clase Object Context implementa la clase **DbContext** (espacio de nombres `Microsoft.EntityFrameworkCore`) y la interfaz **IDbContext** (espacio de nombres `Nop.Data`). Esta interfaz `IDbContext` consta de métodos relacionados con la creación, eliminación y otras acciones personalizadas de la tabla, como ejecutar una consulta SQL sin procesar de acuerdo con el modelo que se agregó previamente en la carpeta`Dominio`.


```cs
public class CountryStateZipObjectContext : DbContext, IDbContext
{
    #region Ctor


    public CountryStateZipObjectContext(DbContextOptions<CountryStateZipObjectContext> options) : base(options)
    {
    }

    #endregion

    #region Utilities

    /// <summary>
    /// Configuración adicional del modelo
    /// </summary>
    /// <param name="modelBuilder">Model muilder</param>
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.ApplyConfiguration(new TaxRateMap());
        base.OnModelCreating(modelBuilder);
    }

    #endregion

    #region Methods

    /// <summary>
    /// Crea un DbSet que se puede utilizar para consultar y guardar instancias de entidad
    /// </summary>
    /// <typeparam name="TEntity">Entity type</typeparam>
    /// <returns>Un conjunto para el tipo de entidad dado</returns>
    public new virtual DbSet<TEntity> Set<TEntity>() where TEntity : BaseEntity
    {
        return base.Set<TEntity>();
    }

    /// <summary>
    ///Genere un script para crear todas las tablas para el modelo actual
    /// </summary>
    /// <returns>A SQL script</returns>
    public virtual string GenerateCreateScript()
    {
        return Database.GenerateCreateScript();
    }

    /// <summary>
    /// Crea una consulta LINQ para el tipo de consulta basada en una consulta SQL sin formato
    /// </summary>
    /// <typeparam name="TQuery">Query type</typeparam>
    /// <param name="sql">The raw SQL query</param>
    /// <param name="parameters">The values to be assigned to parameters</param>
    /// <returns>Un IQueryable que representa la consulta SQL sin procesar</returns>
    public virtual IQueryable<TQuery> QueryFromSql<TQuery>(string sql, params object[] parameters) where TQuery : class
    {
        throw new NotImplementedException();
    }

    /// <summary>
    /// Crea una consulta LINQ para la entidad basada en una consulta SQL sin procesar
    /// </summary>
    /// <typeparam name="TEntity">Entity type</typeparam>
    /// <param name="sql">The raw SQL query</param>
    /// <param name="parameters">The values to be assigned to parameters</param>
    /// <returns>An IQueryable representing the raw SQL query</returns>
    public virtual IQueryable<TEntity> EntityFromSql<TEntity>(string sql, params object[] parameters) where TEntity : BaseEntity
    {
        throw new NotImplementedException();
    }

    /// <summary>
    /// Ejecuta el SQL dado contra la base de datos
    /// </summary>
    /// <param name="sql">The SQL to execute</param>
    /// <param name = "doNotEnsureTransaction"> true - la creación de la transacción no está asegurada; falso: la creación de la transacción está garantizada. </param>
     /// <param name = "timeout"> El tiempo de espera que se utilizará para el comando. Tenga en cuenta que el tiempo de espera del comando es distinto del tiempo de espera de la conexión, que normalmente se establece en la cadena de conexión de la base de datos </param>
     /// <param name = "parameters"> Parámetros para usar con SQL </param>
     /// <returns> El número de filas afectadas </returns>
     public virtual int ExecuteSqlCommand (RawSqlString sql, bool doNotEnsureTransaction = false, int? timeout = null, params object [] parámetros)
    {
        using (var transaction = Database.BeginTransaction())
        {
            var result = Database.ExecuteSqlCommand(sql, parameters);
            transaction.Commit();

            return result;
        }
    }

    /// <summary>
    /// Separar una entidad del contexto
    /// </summary>
    /// <typeparam name="TEntity">Entity type</typeparam>
    /// <param name="entity">Entity</param>
    public virtual void Detach<TEntity>(TEntity entity) where TEntity : BaseEntity
    {
        throw new NotImplementedException();
    }

    /// <summary>
    /// Instalar contexto de objeto
    /// </summary>
    public void Install()
    {
        // crear tablas
        this.ExecuteSqlScript(GenerateCreateScript());
    }

    /// <summary>
    /// Desinstalar el contexto del objeto
    /// </summary>
    public void Uninstall()
    {
        //drop the table
        this.DropPluginTable(nameof(TaxRate));
    }

    #endregion
}
```

Para la operación de tasas impositivas **CRUD**, se crean servicios. En este caso, se crea la interfaz **ICountryStateZipService** y la clase **CountryStateZipService**. Contiene métodos como `InsertTaxRate`,`UpdateTaxRate`, `DeleteTaxRate`,`GetAllTaxRates` y `GetTaxRateById`. Estos nombres de métodos se explican por sí mismos y serán consumidos por los controladores. Se pueden introducir/agregar otros métodos según los requisitos.

### ICountryStateZipService.cs

```cs
public partial interface ICountryStateZipService
{
    /// <summary>
    /// Deletes a tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    void DeleteTaxRate(TaxRate taxRate);

    /// <summary>
    /// Gets all tax rates
    /// </summary>
    /// <returns>Tax rates</returns>
    IPagedList<TaxRate> GetAllTaxRates(int pageIndex = 0, int pageSize = int.MaxValue);

    /// <summary>
    /// Gets a tax rate
    /// </summary>
    /// <param name="taxRateId">Tax rate identifier</param>
    /// <returns>Tax rate</returns>
    TaxRate GetTaxRateById(int taxRateId);

    /// <summary>
    /// Inserts a tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    void InsertTaxRate(TaxRate taxRate);

    /// <summary>
    /// Updates the tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    void UpdateTaxRate(TaxRate taxRate);
}
```

#### CountryStateZipService.cs

```cs
public partial class CountryStateZipService : ICountryStateZipService
{
    #region Fields

    private readonly IEventPublisher _eventPublisher;
    private readonly IRepository<TaxRate> _taxRateRepository;
    private readonly ICacheManager _cacheManager;

    #endregion

    #region Ctor

    /// <summary>
    /// Ctor
    /// </summary>
    /// <param name="eventPublisher">Event publisher</param>
    /// <param name="cacheManager">Cache manager</param>
    /// <param name="taxRateRepository">Tax rate repository</param>
    public CountryStateZipService(IEventPublisher eventPublisher,
        ICacheManager cacheManager,
        IRepository<TaxRate> taxRateRepository)
    {
        _eventPublisher = eventPublisher;
        _cacheManager = cacheManager;
        _taxRateRepository = taxRateRepository;
    }

    #endregion

    #region Methods

    /// <summary>
    /// Deletes a tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    public virtual void DeleteTaxRate(TaxRate taxRate)
    {
        if (taxRate == null)
            throw new ArgumentNullException(nameof(taxRate));

        _taxRateRepository.Delete(taxRate);

        //event notification
        _eventPublisher.EntityDeleted(taxRate);
    }

    /// <summary>
    /// Gets all tax rates
    /// </summary>
    /// <returns>Tax rates</returns>
    public virtual IPagedList<TaxRate> GetAllTaxRates(int pageIndex = 0, int pageSize = int.MaxValue)
    {
        var key = string.Format(ModelCacheEventConsumer.TAXRATE_ALL_KEY, pageIndex, pageSize);
        return _cacheManager.Get(key, () =>
        {
            var query = from tr in _taxRateRepository.Table
                        orderby tr.StoreId, tr.CountryId, tr.StateProvinceId, tr.Zip, tr.TaxCategoryId
                        select tr;
            var records = new PagedList<TaxRate>(query, pageIndex, pageSize);
            return records;
        });
    }

    /// <summary>
    /// Gets a tax rate
    /// </summary>
    /// <param name="taxRateId">Tax rate identifier</param>
    /// <returns>Tax rate</returns>
    public virtual TaxRate GetTaxRateById(int taxRateId)
    {
        if (taxRateId == 0)
            return null;

       return _taxRateRepository.GetById(taxRateId);
    }

    /// <summary>
    /// Inserts a tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    public virtual void InsertTaxRate(TaxRate taxRate)
    {
        if (taxRate == null)
            throw new ArgumentNullException(nameof(taxRate));

        _taxRateRepository.Insert(taxRate);

        //event notification
        _eventPublisher.EntityInserted(taxRate);
    }

    /// <summary>
    /// Updates the tax rate
    /// </summary>
    /// <param name="taxRate">Tax rate</param>
    public virtual void UpdateTaxRate(TaxRate taxRate)
    {
        if (taxRate == null)
            throw new ArgumentNullException(nameof(taxRate));

        _taxRateRepository.Update(taxRate);

        //event notification
        _eventPublisher.EntityUpdated(taxRate);
    }

    #endregion
}
```

Lo último que necesitamos es registrar los servicios y configurar el contexto de la base de datos del complemento al iniciar la aplicación. Para esto, se agrega la carpeta **Infraestructura** que contiene las clases: `DependencyRegister` y `PluginDbStartup`.

La clase **DependencyRegister** implementa la interfaz `IDependencyRegister` (espacio de nombres`Nop.Core.Infrastructure.DependencyManagement`) que tiene el método `Register`.

```cs
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
        builder.RegisterType<FixedOrByCountryStateZipTaxProvider>().As<ITaxProvider>().InstancePerLifetimeScope();
        builder.RegisterType<CountryStateZipService>().As<ICountryStateZipService>().InstancePerLifetimeScope();

        //data context
        builder.RegisterPluginDataContext<CountryStateZipObjectContext>("nop_object_context_tax_country_state_zip");

        //override required repository with our custom context
        builder.RegisterType<EfRepository<TaxRate>>().As<IRepository<TaxRate>>()
            .WithParameter(ResolvedParameter.ForNamed<IDbContext>("nop_object_context_tax_country_state_zip"))
            .InstancePerLifetimeScope();
    }

    /// <summary>
    /// Order of this dependency registrar implementation
    /// </summary>
    public int Order => 1;
}
```

De manera similar, la clase **PluginDbStartup** implementa la interfaz `INopStartup` (espacio de nombres`Nop.Core.Infrastructure`) que tiene los métodos `ConfigureServices` y `Configure`. Para este ejemplo, el contexto del objeto se agrega en el método `ConfigureServices`.

```cs
public class PluginDbStartup : INopStartup
{
    /// <summary>
    /// Add and configure any of the middleware
    /// </summary>
    /// <param name="services">Collection of service descriptors</param>
    /// <param name="configuration">Configuration of the application</param>
    public void ConfigureServices(IServiceCollection services, IConfiguration configuration)
    {
        //add object context
        services.AddDbContext<CountryStateZipObjectContext>(optionsBuilder =>
        {
            optionsBuilder.UseSqlServerWithLazyLoading(services);
        });
    }

    /// <summary>
    /// Configure the using of added middleware
    /// </summary>
    /// <param name="application">Builder for configuring an application's request pipeline</param>
    public void Configure(IApplicationBuilder application)
    {
    }

    /// <summary>
    /// Gets order of this startup configuration implementation
    /// </summary>
    public int Order => 11;
}
```

## Estructura del proyecto del complemento fiscal

![image8](_static/how-to-write-a-tax-plugin-4.20/image8.png)

## Manejo de los métodos "Instalar" y "Desinstalar"

Este paso es opcional. Algunos complementos pueden requerir lógica adicional durante su instalación. Por ejemplo, un complemento puede insertar nuevos recursos de configuración regional o agregar las tablas o los valores de configuración necesarios. Así que abra su implementación de `BasePlugin` y anule los siguientes métodos:

* `Instalar`. Este método se invocará durante la instalación del complemento. Puede inicializar cualquier configuración aquí, insertar nuevos recursos de configuración regional o crear algunas tablas de base de datos nuevas (si es necesario).

```cs
public override void Install()
{
    //database objects
    _objectContext.Install();

    //settings
    _settingService.SaveSetting(new FixedOrByCountryStateZipTaxSettings());

    //locales
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fixed", "Fixed rate");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.TaxByCountryStateZip", "By Country");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategoryName", "Tax category");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Rate", "Rate");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Store", "Store");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Store.Hint", "If an asterisk is selected, then this shipping rate will apply to all stores.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Country", "Country");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Country.Hint", "The country.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.StateProvince", "State / province");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.StateProvince.Hint", "If an asterisk is selected, then this tax rate will apply to all customers from the given country, regardless of the state.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Zip", "Zip");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Zip.Hint", "Zip / postal code. If zip is empty, then this tax rate will apply to all customers from the given country or state, regardless of the zip code.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategory", "Tax category");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategory.Hint", "The tax category.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Percentage", "Percentage");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Percentage.Hint", "The tax rate.");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.AddRecord", "Add tax rate");
    _localizationService.AddOrUpdatePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.AddRecordTitle", "New tax rate");

    base.Install();
}
```

* `Desinstalar`. Este método se invocará durante la desinstalación del complemento. Puede eliminar la configuración, los recursos locales o las tablas de la base de datos previamente inicializados mediante el complemento durante la instalación.

```cs
public override void Uninstall()
{

    //settings
    _settingService.DeleteSetting<FixedOrByCountryStateZipTaxSettings>();

    //fixed rates
    var fixedRates = _taxCategoryService.GetAllTaxCategories()
        .Select(taxCategory => _settingService.GetSetting(string.Format(FixedOrByCountryStateZipDefaults.FixedRateSettingsKey, taxCategory.Id)))
        .Where(setting => setting != null).ToList();
    _settingService.DeleteSettings(fixedRates);

    //database objects
    _objectContext.Uninstall();

    //locales
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fixed");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.TaxByCountryStateZip");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategoryName");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Rate");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Store");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Store.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Country");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Country.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.StateProvince");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.StateProvince.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Zip");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Zip.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategory");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.TaxCategory.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Percentage");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.Fields.Percentage.Hint");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.AddRecord");
    _localizationService.DeletePluginLocaleResource("Plugins.Tax.FixedOrByCountryStateZip.AddRecordTitle");

    base.Uninstall();
}
```

> [!IMPORTANT]
> Si anula uno de estos métodos, no oculte su implementación base -base.Install () y base.Uninstall ().
