---
title: How to write a plugin for nopCommerce
uid: en/developer/plugins/how-to-write-plugin-4.30
author: git.AndreiMaz
contributors: git.skoshelev
---

# Cómo escribir un complemento para nopCommerce

Los complementos se utilizan para ampliar la funcionalidad de nopCommerce. nopCommerce tiene varios tipos de complementos. Por ejemplo, métodos de pago (como PayPal), proveedores de impuestos, métodos de cálculo de métodos de envío (como UPS, USP, FedEx), widgets (como el bloque de 'chat en vivo') y muchos otros. nopCommerce ya se distribuye con muchos complementos diferentes. También puede buscar varios complementos en el [sitio oficial de nopCommerce](https://www.nopcommerce.com/marketplace) para ver si alguien ya ha creado un complemento que se adapte a sus necesidades. De lo contrario, este artículo lo guiará a través del proceso de creación de su propio complemento.

## La estructura del complemento, los archivos requeridos y las ubicaciones

1. Lo primero que debe hacer es crear un nuevo proyecto de "Biblioteca de clases" en la solución. Es una buena práctica colocar todos los complementos en el directorio `\Plugins` en la raíz de su solución (no se mezcle con el subdirectorio\Plugins ubicado en el directorio`\ Nop.Web` que se usa para los complementos ya implementados). Es una buena práctica colocar todos los complementos en la carpeta de la solución "Complementos".

    Un nombre recomendado para un proyecto de complemento es "Nop.Plugin.{Group}.{Name}".{Group} es su grupo de complementos (por ejemplo, "Pago" o "Envío"). {Name} es el nombre de su complemento (por ejemplo, "PayPalStandard"). Por ejemplo, el complemento de pago estándar de PayPal tiene el siguiente nombre: Nop.Plugin.Payments.PayPalStandard. Pero tenga en cuenta que no es un requisito. Y puede elegir cualquier nombre para un complemento. Por ejemplo, "MyGreatPlugin".

    ![p1](_static/how-to-write-plugin-4.30/write_plugin_4.30_1.jpg)

1. Una vez creado el proyecto del complemento, debe abrir su archivo `.csproj` en cualquier editor de texto y reemplazar su contenido por el siguiente:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netcoreapp3.1</TargetFramework>
            <Copyright>SOME_COPYRIGHT</Copyright>
            <Company>YOUR_COMPANY</Company>
            <Authors>SOME_AUTHORS</Authors>
            <PackageLicenseUrl>PACKAGE_LICENSE_URL</PackageLicenseUrl>
            <PackageProjectUrl>PACKAGE_PROJECT_URL</PackageProjectUrl>
            <RepositoryUrl>REPOSITORY_URL</RepositoryUrl>
            <RepositoryType>Git</RepositoryType>
            <OutputPath>..\..\Presentation\Nop.Web\Plugins\PLUGIN_OUTPUT_DIRECTORY</OutputPath>
            <OutDir>$(OutputPath)</OutDir>
            <!--Set this parameter to true to get the dlls copied from the NuGet cache to the output of your    project. You need to set this parameter to true if your plugin has a nuget package to ensure that   the dlls copied from the NuGet cache to the output of your project-->
            <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
        </PropertyGroup>
        <ItemGroup>
            <ProjectReference Include="..\..\Presentation\Nop.Web.Framework\Nop.Web.Framework.csproj" />
            <ClearPluginAssemblies Include="$(MSBuildProjectDirectory)\..\..\Build\ClearPluginAssemblies.proj" />
        </ItemGroup>
        <!-- Este objetivo se ejecuta después del objetivo "Construir" -->
        <Target Name="NopTarget" AfterTargets="Build">
            <!-- Eliminar bibliotecas innecesarias de la ruta de los complementos -->
            <MSBuild Projects="@(ClearPluginAssemblies)" Properties="PluginPath=$(MSBuildProjectDirectory)\ $(OutDir)" Targets="NopClear" />
        </Target>
    </Project>
    ```

    > [!TIP]
     >
     > Donde PLUGIN_OUTPUT_DIRECTORY debe reemplazarse con el nombre del complemento, por ejemplo, Payments.PayPalStandard.
     >
     > Lo hacemos de esta manera para poder usar un nuevo enfoque para agregar referencias de terceros que se introdujo en .NET Core. Pero en realidad no es necesario. Además, las referencias de bibliotecas ya referenciadas se cargarán automáticamente. Por eso es muy conveniente.

1. El siguiente paso es crear un archivo `plugin.json` requerido para cada complemento. Este archivo contiene metainformación que describe su complemento. Simplemente copie este archivo de cualquier otro complemento existente y modifíquelo según sus necesidades. Por ejemplo, el complemento de pago estándar de PayPal tiene el siguiente archivo `plugin.json`:

    ```json
    {
        "Group": "Payment methods",
        "FriendlyName": "PayPal Standard",
        "SystemName": "Payments.PayPalStandard",
        "Version": "1.60",
        "SupportedVersions": [ "4.30" ],
        "Author": "nopCommerce team",
        "DisplayOrder": 1,
        "FileName": "Nop.Plugin.Payments.PayPalStandard.dll",
        "Description": "This plugin allows paying with PayPal Standard"
    }
    ```

    > [!NOTE]
    > Además, el archivo `plugin.json` puede contener los siguientes campos:
    >
    > * **LimitedToStores**: la lista de identificadores de tiendas en las que está disponible este complemento. Si está vacío, este complemento está disponible en todas las tiendas.
    > * **LimitedToCustomerRoles**: la lista de identificadores de roles de clientes para los que está disponible este complemento. Si está vacío, este complemento está disponible para todos.
    > * **DependsOnSystemNames**: la lista de nombres de sistema de complementos de los que depende este complemento

    En realidad, todos los campos son autodescriptivos, pero aquí hay algunas notas. El campo **SystemName** debe ser único. El campo **Versión** es un número de versión de su complemento; puede configurarlo en cualquier valor que desee. El campo **SupportedVersions** puede contener una lista de versiones de nopCommerce compatibles separadas por comas (asegúrese de que la versión actual de nopCommerce esté incluida en esta lista; de lo contrario, no se cargará). El campo **FileName** tiene el siguiente formato Nop.Plugin. {Group}. {Name} .dll (es el nombre de archivo de ensamblaje de su complemento). Asegúrese de que la propiedad *"Copiar en el directorio de salida"* de este archivo esté establecida en *"Copiar si es más reciente"*.

    ![p2](_static/how-to-write-plugin-4.30/write_plugin_4.30_2.jpg)

1. El último paso requerido es crear una clase que implemente la interfaz **IPlugin** (espacio de nombres Nop.Services.Plugins). nopCommerce tiene la clase **BasePlugin** que ya implementa algunos métodos de IPlugin y le permite evitar la duplicación del código fuente. nopCommerce también le proporciona algunas interfaces específicas derivadas de IPlugin. Por ejemplo, tenemos la interfaz "IPaymentMethod" que se utiliza para crear nuevos complementos de métodos de pago. Contiene algunos métodos que son específicos solo para métodos de pago como *ProcessPayment ()* o *GetAdditionalHandlingFee ()*. Actualmente, nopCommerce tiene las siguientes interfaces de complementos específicas:

> [!IMPORTANT]
>
> Nota importante: después de la construcción de cada proyecto, limpie la solución antes de realizar cambios. Algunos recursos se almacenarán en caché y pueden provocar la locura del desarrollador.

> [!IMPORTANT]
>
> Es posible que deba reconstruir su solución después de agregar su complemento. Si no ve los archivos DLL para su complemento en Nop.Web\Plugins\PLUGIN_OUTPUT_DIRECTORY, debe reconstruir su solución. nopCommerce no incluirá su complemento en la página Complementos locales si sus DLL no existen en la carpeta correcta en Nop.Web.

## Manejo de solicitudes. Controladores, modelos y vistas

Ahora puede ver el complemento yendo a **Área de administración → Configuración → Complementos locales**. Pero como adivinó, nuestro complemento no hace nada. Ni siquiera tiene una interfaz de usuario para su configuración. Creemos una página para configurar el complemento.

Lo que tenemos que hacer ahora es crear un controlador, un modelo y una vista.

1. Los controladores MVC son responsables de responder a las solicitudes realizadas en un sitio web ASP.NET MVC. Cada solicitud del navegador se asigna a un controlador en particular.
1. Una vista contiene el marcado HTML y el contenido que se envía al navegador. Una vista es el equivalente a una página cuando se trabaja con una aplicación ASP.NET MVC.
1. Un modelo MVC contiene toda la lógica de su aplicación que no está contenida en una vista o un controlador.

Puede encontrar más información sobre el patrón MVC [aquí](https://docs.microsoft.com/aspnet/core/mvc/overview?view=aspnetcore-3.1).

Así que comencemos:

- **Crea el modelo**. Agregue una carpeta **Modelos** en el nuevo complemento y luego agregue una nueva clase de modelo que se adapte a sus necesidades.
- **Crear la vista**. Agregue una carpeta **Vistas** en el nuevo complemento y luego agregue un archivo cshtml llamado `Configure.cshtml`. La propiedad **"Acción de compilación"** del archivo de vista se establece en **"Contenido"**, y la propiedad **"Copiar en el directorio de salida"** se establece en **"Copiar siempre"**. Tenga en cuenta que la página de configuración debe utilizar el diseño "_ConfigurePlugin".
- También asegúrese de tener el archivo `_ViewImports.cshtml` en su directorio \ Views. Puede copiarlo desde cualquier otro complemento existente.
- **Crea el controlador**. Agregue una carpeta **Controllers** en el nuevo complemento y luego agregue una nueva clase de controlador. Una buena práctica es nombrar los controladores de complementos `{Grupo} {Nombre} Controller.cs`. Por ejemplo, PaymentPayPalStandardController. Por supuesto, no es un requisito nombrar a los controladores de esta manera (sino solo una recomendación). Luego, cree un método de acción apropiado para la página de configuración (en el área de administración). Vamos a nombrarlo *"Configurar"*. Prepara una clase de modelo y pásala a la siguiente vista usando una ruta de vista física: `~ / Plugins / {PluginOutputDirectory} / Views / Configure.cshtml`.
- Utilice los siguientes atributos para su método de acción:

    ```csharp
    [AuthorizeAdmin] //confirma el acceso al panel de administración
    [Area(AreaNames.Admin)] //especifica el área que contiene un controlador o acción
    ```

    Por ejemplo, abra el complemento de pago PayPalStandard y observe su implementación de PaymentPayPalStandardController.

Luego, para cada complemento que tenga una página de configuración, debe especificar una URL de configuración. La clase base denominada BasePlugin tiene el método GetConfigurationPageUrl que devuelve una URL de configuración:

```csharp
public override string GetConfigurationPageUrl()
{
    return $"{_webHelper.GetStoreLocation()}Admin/{CONTROLLER_NAME}/{ACTION_NAME}";
}
```

Donde *{CONTROLLER_NAME}* es el nombre de su controlador y *{ACTION_NAME}* es el nombre de la acción (generalmente es "Configurar").

Una vez que haya instalado su complemento y agregado el método de configuración, encontrará un enlace para configurar su complemento en **Admin → Configuración → Complementos locales**.

> [!TIP]
>
> Consejo: la forma más sencilla de completar los pasos descritos anteriormente es abrir cualquier otro complemento y copiar estos archivos en su proyecto de complemento. Luego simplemente cambie el nombre de las clases y directorios apropiados.

Por ejemplo, la estructura del proyecto del complemento PayPalStandard se parece a la siguiente imagen:

![p3](_static/how-to-write-plugin-4.30/write_plugin_4.30_3.jpg)

## Manejo de los métodos "Instalar", "Desinstalar" y "Actualizar"

Este paso es opcional. Algunos complementos pueden requerir lógica adicional durante la instalación del complemento. Por ejemplo, un complemento puede insertar nuevos recursos de configuración regional. Entonces, abra su implementación de IPlugin (en la mayoría de los casos se derivará de la clase BasePlugin) y anule los siguientes métodos:

1. **Instalar**. Este método se invocará durante la instalación del complemento. Puede inicializar cualquier configuración aquí, insertar nuevos recursos de configuración regional o crear algunas tablas de base de datos nuevas (si es necesario).
1. **Desinstalar**. Este método se invocará durante la desinstalación del complemento.
1. **Actualización**. Este método se invocará durante la actualización del complemento (cuando se cambie su versión en el archivo `plugin.json`).

>[!IMPORTANT]
>
> Nota importante: si anula uno de estos métodos, no oculte su implementación básica.

Por ejemplo, el método "Install" anulado debe incluir la siguiente llamada al método: *base.Install ()*. El método "Instalar" del complemento PayPalStandard se parece al código siguiente

```csharp
public override void Install()
{
    var settings = new PayPalStandardPaymentSettings()
    {
        UseSandbox = true
    };
    _settingService.SaveSetting(settings);
    ...
    base.Install();
}
```

> [!TIP]
>
> La lista de complementos instalados se encuentra en `\App_Data\plugins.json`. La lista se crea durante la instalación.

## Rutas

Aquí veremos cómo registrar rutas de complementos. El enrutamiento de ASP.NET Core es responsable de asignar las solicitudes entrantes del navegador a acciones particulares del controlador MVC. Puede encontrar más información sobre el enrutamiento [aquí](https://docs.microsoft.com/aspnet/core/fundamentals/routing). Entonces sigue los siguientes pasos:

Si necesita agregar alguna ruta personalizada, cree el archivo `RouteProvider.cs`. Informa al sistema nopCommerce sobre las rutas de los complementos. Por ejemplo, la siguiente clase RouteProvider agrega una nueva ruta a la que se puede acceder abriendo su navegador web y navegando a la URL `http://www.yourStore.com/Plugins/PaymentPayPalStandard/PDTHandler` (utilizada por el complemento de PayPal):

```csharp
public partial class RouteProvider : IRouteProvider
{
    public void RegisterRoutes(IEndpointRouteBuilder endpointRouteBuilder)
    {
        //PDT
        endpointRouteBuilder.MapControllerRoute("Plugin.Payments.PayPalStandard.PDTHandler", "Plugins/PaymentPayPalStandard/PDTHandler",
                new { controller = "PaymentPayPalStandard", action = "PDTHandler" });
    }
    public int Priority => -1;
}
```

## Actualizar nopCommerce puede romper los complementos

Algunos complementos pueden quedar desactualizados y ya no funcionan con la versión más reciente de nopCommerce. Si tiene problemas después de actualizar a la versión más reciente, elimine el complemento y visite el sitio web oficial de nopCommerce para ver si hay una versión más nueva disponible. Muchos autores de complementos actualizarán sus complementos para adaptarse a la versión más nueva, sin embargo, algunos no lo harán y su complemento se volverá obsoleto con las mejoras en nopCommerce. Pero en la mayoría de los casos, simplemente puede abrir un archivo `plugin.json` apropiado y actualizar el campo **SupportedVersions**.

## Conclusión

Con suerte, esto lo ayudará a comenzar con nopCommerce y lo preparará para crear complementos más elaborados.

## Plantilla de complemento

Puede utilizar nuestra plantilla de Visual Studio para nuevos complementos de nopCommerce. Puede ahorrar mucho tiempo a los desarrolladores, porque ahora no tienen que realizar manualmente todos los pasos iniciales. Como creación de carpetas (controladores, vistas, modelos, etc.), otros archivos necesarios (DependencyRegistrar.cs, _ViewImports.cshtml, ObjectContex, plugin.json, etc.), configuración, referencias de proyectos, etc. Encuéntrelo y las instrucciones de instalación [aquí](https://github.com/nopSolutions/nopCommerce-plugin-template-VS/)
