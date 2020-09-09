---
title: How to write a plugin for nopCommerce
uid: en/developer/plugins/how-to-write-plugin-4.00
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Cómo escribir un complemento para nopCommerce 4.00

> En informática, un complemento (o complemento) es un conjunto de componentes de software que agregan capacidades específicas a una aplicación de software más grande (Wikipedia).

Los complementos se utilizan para ampliar la funcionalidad de nopCommerce. nopCommerce tiene varios tipos de complementos. Por ejemplo, métodos de pago (como PayPal), proveedores de impuestos, métodos de cálculo de métodos de envío (como UPS, USP, FedEx), widgets (como el bloque de 'chat en vivo') y muchos otros. nopCommerce ya se distribuye con muchos complementos diferentes. También puede buscar varios complementos en el [sitio oficial de nopCommerce](https://www.nopcommerce.com/marketplace) para ver si alguien ya ha creado un complemento que se adapte a sus necesidades. De lo contrario, este artículo lo guiará a través del proceso de creación de su propio complemento.

## La estructura del complemento, los archivos necesarios y las ubicaciones

1. Lo primero que debe hacer es crear un nuevo proyecto de "Biblioteca de clases" en la solución. Es una buena práctica colocar todos los complementos en el directorio `\ Complementos` en la raíz de su solución (no se mezcle con el subdirectorio\Complementos ubicado en el directorio` \ Nop.Web` que se usa para complementos ya implementados). Es una buena práctica colocar todos los complementos en la carpeta de la solución "Complementos" (puede encontrar más información sobre las carpetas de la solución [aquí](http://msdn.microsoft.com/library/sx2027y2.aspx)).

    Un nombre recomendado para un proyecto de complemento es "Nop.Plugin. {Group}. {Name}". {Group} es su grupo de complementos (por ejemplo, "Pago" o "Envío"). {Name} es el nombre de su complemento (por ejemplo, "PayPalStandard"). Por ejemplo, el complemento de pago estándar de PayPal tiene el siguiente nombre: Nop.Plugin.Payments.PayPalStandard. Pero tenga en cuenta que no es un requisito. Y puede elegir cualquier nombre para un complemento. Por ejemplo, "MyGreatPlugin".

    ![p1](_static/how-to-write-plugin-4.00/write_plugin_4.00_1.jpg)

1. Once the plugin project is created you have to open its `.csproj` file in any text editor and replace its content with the following one:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
     <PropertyGroup>
       <TargetFramework>net461</TargetFramework>
     </PropertyGroup>
     <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
       <OutputPath>..\..\Presentation\Nop.Web\Plugins\PLUGIN_OUTPUT_DIRECTORY</OutputPath>
       <OutDir>$(OutputPath)</OutDir>
     </PropertyGroup>
     <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
       <OutputPath>..\..\Presentation\Nop.Web\Plugins\PLUGIN_OUTPUT_DIRECTORY</OutputPath>
       <OutDir>$(OutputPath)</OutDir>
     </PropertyGroup>
     <!-- This target execute after "Build" target -->
     <Target Name="NopTarget" AfterTargets="Build">
       <!-- Delete unnecessary libraries from plugins path -->
       <MSBuild Projects="$(MSBuildProjectDirectory)\..\..\Build\ClearPluginAssemblies.proj"    Properties="PluginPath=$(MSBuildProjectDirectory)\$(OutDir)" Targets="NopClear" />
     </Target>
    </Project>
    ```

    Donde PLUGIN_OUTPUT_DIRECTORY debe reemplazarse con el nombre del complemento, por ejemplo, Payments.PayPalStandard.

     Lo hacemos de esta manera para poder usar un nuevo enfoque para agregar referencias de terceros que se introdujo en .NET Core. Pero en realidad no es necesario. Además, las referencias de bibliotecas ya referenciadas se cargarán automáticamente. Por eso es muy conveniente.

1. El siguiente paso es crear un archivo `plugin.json` requerido para cada complemento. Este archivo contiene metainformación que describe su complemento. Simplemente copie este archivo de cualquier otro complemento existente y modifíquelo según sus necesidades. Por ejemplo, el complemento de pago estándar de PayPal tiene el siguiente archivo `plugin.json`:

    ```json
    {
     "Group": "Payment methods",
     "FriendlyName": "PayPal Standard",
     "SystemName": "Payments.PayPalStandard",
     "Version": "1.42",
     "SupportedVersions": [ "4.00" ],
     "Author": "nopCommerce team",
     "DisplayOrder": 1,
     "FileName": "Nop.Plugin.Payments.PayPalStandard.dll",
     "Description": "This plugin allows paying with PayPal Standard"
    }
    ```

    En realidad, todos los campos son autodescriptivos, pero aquí hay algunas notas. El campo **SystemName** debe ser único. El campo ** Versión ** es un número de versión de su complemento; puede configurarlo en cualquier valor que desee. El campo **SupportedVersions** puede contener una lista de versiones de nopCommerce compatibles separadas por comas (asegúrese de que la versión actual de nopCommerce esté incluida en esta lista, de lo contrario, no se cargará). El campo **FileName** tiene el siguiente formato * Nop.Plugin. {Group}. {Name} .dll * (es el nombre de archivo de ensamblaje de su complemento). Asegúrese de que la propiedad "Copiar en el directorio de salida" de este archivo esté establecida en "Copiar si es más reciente".

    ![p2](_static/how-to-write-plugin-4.00/write_plugin_4.00_2.jpg)

1. El último paso requerido es crear una clase que implemente la interfaz IPlugin (espacio de nombres Nop.Core.Plugins). nopCommerce tiene la clase BasePlugin que ya implementa algunos métodos IPlugin y le permite evitar la duplicación del código fuente. nopCommerce también le proporciona algunas interfaces específicas derivadas de IPlugin. Por ejemplo, tenemos la interfaz "IPaymentMethod" que se utiliza para crear nuevos complementos de métodos de pago. Contiene algunos métodos que son específicos solo para métodos de pago como ProcessPayment () o GetAdditionalHandlingFee (). Actualmente, nopCommerce tiene las siguientes interfaces de complementos específicas:

    - **IExternalAuthenticationMethod**. Se utiliza para crear métodos de autenticación externos como Facebook, Twitter, OpenID, etc.
    - **IWidgetPlugin**. Te permite crear widgets. Los widgets se representan en algunas partes de su sitio. Por ejemplo, puede ser un bloque de "chat en vivo" en la columna izquierda de su sitio.
    - **IExchangeRateProvider**. Se utiliza para obtener el tipo de cambio de moneda.
    - **IDiscountRequirementRule**. Le permite crear nuevas reglas de descuento como "El país de facturación de un cliente debe ser ...".
    - **IPaymentMethod**. Complementos que se utilizan para el procesamiento de pagos.
    - **IShippingRateComputationMethod**. Estos complementos se utilizan para recuperar métodos de entrega aceptados y tarifas de envío adecuadas. Por ejemplo, UPS, UPS, FedEx, etc.
    - **ITaxProvider**. Los proveedores de impuestos se utilizan para obtener tasas impositivas.

    Si su complemento no se ajusta a ninguna de estas interfaces, utilice la interfaz "IMiscPlugin".

> [!IMPORTANTE]
>
> Después de la construcción de cada proyecto, limpie la solución antes de realizar cambios. Algunos recursos se almacenarán en caché y pueden provocar la locura del desarrollador.

## Manejo de solicitudes. Controladores, modelos y vistas

Ahora puede ver el complemento yendo a ** Área de administración → Configuración → Complementos **. Pero como adivinó, nuestro complemento no hace nada. Ni siquiera tiene una interfaz de usuario para su configuración. Creemos una página para configurar el complemento.

Lo que tenemos que hacer ahora es crear un controlador, un modelo y una vista.

- Los controladores MVC son responsables de responder a las solicitudes realizadas en un sitio web ASP.NET MVC. Cada solicitud del navegador se asigna a un controlador en particular.
- Una vista contiene el marcado HTML y el contenido que se envía al navegador. Una vista es el equivalente a una página cuando se trabaja con una aplicación ASP.NET MVC.
- Un modelo MVC contiene toda la lógica de su aplicación que no está contenida en una vista o un controlador.

Puede encontrar más información sobre el patrón MVC [aquí] (http://www.asp.net/mvc/tutorials/older-versions/overview/understanding-models-views-and-controllers-cs).

Así que comencemos:

- **Crea el modelo**. Agregue una carpeta de modelos en el nuevo complemento y luego agregue una nueva clase de modelo que se adapte a sus necesidades.
- **Crear la vista**. Agregue una carpeta Vistas en el nuevo complemento y luego agregue un archivo cshtml llamado `Configure.cshtml`. La propiedad "Acción de compilación" del archivo de vista se establece en "Contenido" y la propiedad "Copiar en el directorio de salida" se establece en "Copiar si es más reciente". Tenga en cuenta que la página de configuración debe utilizar el diseño "_ConfigurePlugin". También asegúrese de tener el archivo_ViewImports en su directorio \ Views. Puede copiarlo desde cualquier otro complemento existente.
- **Crea el controlador**. Agregue una carpeta de controladores en el nuevo complemento y luego agregue una nueva clase de controlador. Una buena práctica es nombrar los controladores de complementos `{Grupo} {Nombre} Controller.cs`. Por ejemplo, PaymentPayPalStandardController. Por supuesto, no es un requisito nombrar los controladores de esta manera (sino solo una recomendación). Luego, cree un método de acción apropiado para la página de configuración (en el área de administración). Vamos a llamarlo "Configurar". Prepare una clase de modelo y páselo a la siguiente vista usando una ruta de vista física: - `~ / Plugins / {PluginOutputDirectory} / Views / Configure.cshtml`.
- Utilice los siguientes atributos para su método de acción:

    ```csharp
    [AuthorizeAdmin] //confirma el acceso al panel de administración
    [Area(AreaNames.Admin)] //especifica el área que contiene un controlador o acción
    ```

    Por ejemplo, abra el complemento de pago PayPalStandard y observe su implementación de PaymentPayPalStandardController.

Luego, para cada complemento que tenga una página de configuración, debe especificar una URL de configuración. La clase base denominada BasePlugin tiene el método GetConfigurationPageUrl que devuelve una URL de configuración:

```csharp
return $"{_webHelper.GetStoreLocation()}Admin/ControllerName/ActionName";
```

Donde ControllerName es un nombre del controlador y ActionName es un nombre de acción (normalmente es "Configurar").

Una vez que haya instalado su plugin y añadido el método de configuración, encontrará un enlace para configurar su plugin en Admin .

> [!CONSEJO]
>
> La forma más fácil de completar los pasos descritos anteriormente es abrir cualquier otro plugin y copiar estos archivos en su proyecto de plugin. A continuación, simplemente cambie el nombre de las clases y directorios adecuados.

Por ejemplo, la estructura del proyecto del plugin PayPalStandard se parece a la imagen de abajo:

![p3](_static/cómo escribir-plugin-4.00/write_plugin_4.00_3.jpg)



## Manejo de los métodos "Instalar" y "Desinstalar"

Este paso es opcional. Algunos complementos pueden requerir lógica adicional durante la instalación del complemento. Por ejemplo, un complemento puede insertar nuevos recursos de configuración regional. Así que abra su implementación de IPlugin (en la mayoría de los casos se derivará de la clase BasePlugin) y anule los siguientes métodos:

- Instalar en pc. Este método se invocará durante la instalación del complemento. Puede inicializar cualquier configuración aquí, insertar nuevos recursos de configuración regional o crear algunas tablas de base de datos nuevas (si es necesario).
- Desinstalar. Este método se invocará durante la desinstalación del complemento.

> [!IMPORTANTE]
> 
> Si anula uno de estos métodos, no oculte su implementación base.

Por ejemplo, el método "Install" anulado debe incluir la siguiente llamada al método: base.Install (). El método "Instalar" del complemento PayPalStandard se parece al código siguiente

```csharp
public override void Install()
{
    var settings = new PayPalStandardPaymentSettings()
    {
        UseSandbox = true
    };
    _settingService.SaveSetting(settings);
    base.Install();
}
```

> [!SUGERENCIA]
>
> La lista de complementos instalados se encuentra en `\ App_Data \ installedPlugins.json`. La lista se crea durante la instalación.

## Rutas

Aquí veremos cómo registrar rutas de complementos. El enrutamiento de ASP.NET Core es responsable de asignar las solicitudes entrantes del navegador a determinadas acciones del controlador MVC. Puede encontrar más información sobre el enrutamiento [aquí] (https://docs.microsoft.com/aspnet/core/fundamentals/routing). Así que sigue los siguientes pasos:

-Si necesita agregar alguna ruta personalizada, cree el archivo `RouteProvider.cs`. Informa al sistema nopCommerce sobre las rutas de los complementos. Por ejemplo, la siguiente clase RouteProvider agrega una nueva ruta a la que se puede acceder abriendo su navegador web y navegando a la URL `http: // www.yourStore.com / Plugins / PaymentPayPalStandard / PDTHandler` (utilizada por el complemento de PayPal):

    ```csharp
    public partial class RouteProvider : IRouteProvider
    {
        public void RegisterRoutes(IRouteBuilder routeBuilder)
        {
             routeBuilder.MapRoute("Plugin.Payments.PayPalStandard.PDTHandler", "Plugins/   PaymentPayPalStandard/PDTHandler",
             new { controller = "PaymentPayPalStandard", action = "PDTHandler" });
        }
        public int Priority
        {
            get
            {
                return -1;
            }
        }
    }
    ```

## Actualizar nopCommerce puede romper los complementos

Algunos complementos pueden quedar desactualizados y ya no funcionan con la versión más reciente de nopCommerce. Si tiene problemas después de actualizar a la versión más reciente, elimine el complemento y visite el sitio web oficial de nopCommerce para ver si hay una versión más nueva disponible. Muchos autores de complementos actualizarán sus complementos para adaptarse a la versión más reciente, sin embargo, algunos no lo harán y su complemento se volverá obsoleto con las mejoras en nopCommerce. Pero en la mayoría de los casos, simplemente puede abrir un archivo `plugin.json` apropiado y actualizar el campo ** SupportedVersions **.

## Conclusión

Con suerte, esto lo ayudará a comenzar con nopCommerce y lo preparará para crear complementos más elaborados.
