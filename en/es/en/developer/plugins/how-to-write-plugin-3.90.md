---
title: How to write a plugin for nopCommerce
uid: en/developer/plugins/how-to-write-plugin-3.90
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Cómo escribir un plugin para nopCommerce 3.90 (y versiones anteriores)

> En informática, un plugin (o plugin) es un conjunto de componentes de software que agregan capacidades específicas a una aplicación de software más grande (Wikipedia).

Los plugins se utilizan para ampliar la funcionalidad de nopCommerce. nopCommerce tiene varios tipos de plugins. Por ejemplo, métodos de pago (como PayPal), proveedores de impuestos, métodos de cálculo de métodos de envío (como UPS, USP, FedEx), widgets (como el bloque de 'chat en vivo') y muchos otros. nopCommerce ya se distribuye con muchos plugins diferentes. También puede buscar varios plugins en el [sitio oficial de nopCommerce](https://www.nopcommerce.com/marketplace) para ver si alguien ya ha creado un plugin que se adapte a sus necesidades. De lo contrario, este artículo lo guiará a través del proceso de creación de su propio plugin.

## La estructura del plugin, los archivos necesarios y las ubicaciones

1. Lo primero que debe hacer es crear un nuevo proyecto de "Biblioteca de clases" en la solución. Es una buena práctica colocar todos los plugins en el directorio `\ plugins` en la raíz de su solución (no se mezcle con el subdirectorio \ plugins ubicado en el directorio` \ Nop.Web` que se usa para plugins ya implementados). Es una buena práctica colocar todos los plugins en la carpeta de la solución "plugins" (puede encontrar más información sobre las carpetas de la solución [aquí](http://msdn.microsoft.com/library/sx2027y2.aspx)).

    Un nombre recomendado para un proyecto de plugin es "Nop.Plugin. {Group}. {Name}". {Group} es su grupo de plugins (por ejemplo, "Pago" o "Envío"). {Name} es el nombre de su plugin (por ejemplo, "PayPalStandard"). Por ejemplo, el plugin de pago estándar de PayPal tiene el siguiente nombre: Nop.Plugin.Payments.PayPalStandard. Pero tenga en cuenta que no es un requisito. Y puede elegir cualquier nombre para un plugin. Por ejemplo, "MyGreatPlugin".

    ![p1](_static/how-to-write-plugin-3.90/write_plugin_3.90_4.jpg)

1. Una vez que se crea el proyecto del plugin, actualice la ruta de salida de la compilación del proyecto. Configúrelo en               `.. \ .. \Presentation\Nop.Web\Plugins\ {Group}.{Name}`. Por ejemplo, el plugin de pago Authorize.NET tiene la siguiente ruta de salida: `.. \ .. \ Presentation\Nop.Web\ Plugins\ Payments.AuthorizeNet`. Una vez hecho esto, las DLL de plugins correspondientes se copiarán automáticamente en el directorio `\Presentation\ Nop.Web \ Plugins` que es buscado por el núcleo de nopCommerce para plugins válidos. Pero tenga en cuenta que tampoco es un requisito. Y puede elegir cualquier nombre de directorio de salida para un plugin.

    ![p1](_static/how-to-write-plugin-3.90/write_plugin_3.90_1.jpg)

    - En el menú Proyecto, haga clic en Propiedades.
    - Haga clic en la pestaña Crear.
    - Haga clic en el botón Examinar junto al cuadro Ruta de salida y seleccione un nuevo directorio de salida de compilación.

     Debe seguir los pasos descritos anteriormente para todas las configuraciones existentes ("Depurar" y "Liberar").

1. El siguiente paso es crear un archivo `Description.txt` requerido para cada plugin. Este archivo contiene metainformación que describe su plugin. Simplemente copie este archivo de cualquier otro plugin existente y modifíquelo según sus necesidades. Por ejemplo, el plugin de pago estándar de PayPal tiene el siguiente archivo `Description.txt`:

    ```txt
    Group: Payment methods
    FriendlyName: PayPal Standard
    SystemName: Payments.PayPalStandard
    Version: 1.28
    SupportedVersions: 3.90
    Author: nopCommerce team
    DisplayOrder: 1
    FileName: Nop.Plugin.Payments.PayPalStandard.dll
    Description: This plugin allows paying with PayPal Standard
    ```

    En realidad, todos los campos son autodescriptivos, pero aquí hay algunas notas. El campo **SystemName** debe ser único. El campo **Versión** es un número de versión de su plugin; puede configurarlo en cualquier valor que desee. El campo **SupportedVersions** puede contener una lista de las versiones de nopCommerce compatibles separadas por comas (asegúrese de que la versión actual de nopCommerce esté incluida en esta lista; de lo contrario, no se cargará). El campo **FileName** tiene el siguiente formato *Nop.Plugin. {Group}. {Name} .dll* (es el nombre de archivo de ensamblaje de su plugin). Asegúrese de que la propiedad "Copiar en el directorio de salida" de este archivo esté establecida en "Copiar si es más reciente".

    ![p2](_static/how-to-write-plugin-3.90/write_plugin_3.90_2.jpg)

1. También debe crear un archivo web.config y asegurarse de que se copia en la salida. Simplemente cópielo desde cualquier plugin existente.

> [!IMPORTANT]
>
> En adelante, asegúrese de que las propiedades "Copiar local" de todas las referencias de ensamblado de terceros (incluidas las bibliotecas principales como Nop.Services.dll o Nop.Web.Framework.dll) estén establecidas en "False" (no copie)

1. El último paso necesario es crear una clase que implemente la interfaz IPlugin (espacio de nombres Nop.Core.Plugins). nopCommerce tiene la clase BasePlugin que ya implementa algunos métodos IPlugin y le permite evitar la duplicación de código fuente. Por ejemplo, tenemos la interfaz "IPaymentMethod" que se utiliza para crear nuevos plugins de métodos de pago. Contiene algunos métodos que son específicos solo para métodos de pago como ProcessPayment() o GetAdditionalHandlingFee(). Actualmente nopCommerce tiene las siguientes interfaces de plugins específicas:

- **IExternalAuthenticationMethod**. Se utiliza para crear métodos de autenticación externos como Facebook, Twitter, OpenID, etc.
- **IWidgetPlugin**. Le permite crear widgets. Los widgets se representan en algunas partes de su sitio. Por ejemplo, puede ser un bloque "Chat en vivo" en la columna izquierda de su sitio.
- **IExchangeRateProvider**. Se utiliza para obtener el tipo de cambio de divisas.
- **IDiscountRequirementRule**. Le permite crear nuevas reglas de descuento como "El país de facturación de un cliente debe ser..."
- **IPaymentMethod**. plugins que se utilizan para el procesamiento de pagos.
- **IShippingRateComputationMethod**. Estos plugins se utilizan para recuperar métodos de entrega aceptados y tarifas de envío adecuadas. Por ejemplo, UPS, UPS, FedEx, etc.
- **ITaxProvider**. Los proveedores de impuestos se utilizan para obtener tasas de impuestos.

    uIf your plugin doesn't fit any of these interfaces, then use the "IMiscPlgin" interface.

>[!IMPORTANT]
>
> Después de cada compilación del proyecto, limpie la solución antes de realizar cambios. Algunos recursos se almacenarán en caché y pueden provocar locuras de los desarrolladores.

## Manejo de solicitudes. Controladores, modelos y vistas

Ahora puedes ver el plugin yendo a **Admin area > Configuración > Plugins**. Pero como adivinó nuestro plugin no hace nada. Ni siquiera tiene una interfaz de usuario para su configuración. Vamos a crear una página para configurar el plugin.

Lo que tenemos que hacer ahora es crear un controlador, un modelo y una vista.

- Los controladores MVC son responsables de responder a las solicitudes realizadas en un sitio web MVC ASP.NET. Cada solicitud del explorador se asigna a un controlador determinado.
- Una vista contiene el marcado HTML y el contenido que se envía al navegador. Una vista es el equivalente de una página cuando se trabaja con una aplicación MVC ASP.NET.
- Un modelo MVC contiene toda la lógica de la aplicación que no está contenida en una vista o un controlador.

Puede encontrar más información sobre el patrón MVC [aquí](http://www.asp.net/mvc/tutorials/older-versions/overview/understanding-models-views-and-controllers-cs).

So let's start:

- **Crea el modelo**. Agregue una carpeta de modelos en el nuevo plugin y luego agregue una nueva clase de modelo que se adapte a sus necesidades.
- **Crear la vista**. Agregue una carpeta Vistas en el nuevo plugin, luego agregue una carpeta {Nombre} (donde {Nombre} es el nombre de su plugin), y finalmente agregue un archivo cshtml llamado `Configure.cshtml`. Nota importante: para las versiones 2.00-3.30, la vista debe marcarse como un recurso incrustado. Y a partir de las vistas de la versión 3.40, asegúrese de que la propiedad "Acción de compilación" del archivo de vista esté establecida en "Contenido" y que la propiedad "Copiar en el directorio de salida" esté establecida en "Copiar si es más reciente".
- **Crea el controlador**. Agregue una carpeta de controladores en el nuevo plugin y luego agregue una nueva clase de controlador. Una buena práctica es nombrar los controladores de plugins `{Grupo} {Nombre} Controller.cs`. Por ejemplo, PaymentAuthorizeNetController. Por supuesto, no es un requisito nombrar los controladores de esta manera (sino solo una recomendación). Luego, cree un método de acción apropiado para la página de configuración (en el área de administración). Vamos a llamarlo "Configurar". Prepare una clase modelo y páselo a la siguiente vista. Para las versiones 2.00-3.30 de nopCommerce, debe pasar la ruta de vista incrustada: "Nop.Plugin. {Group}. {Name} .Views. {Group} {Name} .Configure". Y a partir de la versión 3.40 de nopCommerce, debe pasar la ruta de la vista física: `~ / Plugins / {PluginOutputDirectory} / Views / {ControllerName} / Configure.cshtml`. Por ejemplo, abra el plugin de pago Authorize.NET y observe su implementación de PaymentAuthorizeNetController.

   > [!tip]
>
> - La forma más fácil de completar los pasos descritos anteriormente es abrir cualquier otro plugin y copiar estos archivos en su proyecto de plugin. A continuación, simplemente cambie el nombre de las clases y directorios adecuados.
> -Si desea limitar el acceso a un determinado método de acción del controlador a los administradores (propietarios de la tienda), a continuación, simplemente márquelo con [AdminAuthorize] atributo.

Por ejemplo, la estructura del proyecto de Authorize.NET plugin se parece a la imagen de abajo

![p3](_static/how-to-write-plugin-3.90/write_plugin_3.90_3.jpg)

## Rutas

Ahora necesitamos registrar rutas de plugin apropiadas. ASP.NET enrutamiento es responsable de asignar solicitudes de explorador entrantes a acciones de controlador MVC concretas. Puede encontrar más información sobre el enrutamiento [aquí](http://www.asp.net/mvc/tutorials/older-versions/controllers-and-routing/asp-net-mvc-routing-overview-cs). Así que sigue los siguientes pasos:

- Algunas de las interfaces específicas del plugin (descritas anteriormente) y la interfaz "IMiscPlugin" tienen el siguiente método: "GetConfigurationRoute". Debe devolver una ruta a una acción del controlador que se utiliza para la configuración del plugin. Implemente el método "GetConfigurationRoute" de la interfaz del plugin. Este método informa a nopCommerce sobre qué ruta se utiliza para la configuración del plugin. Si el plugin no tiene una página de configuración, "GetConfigurationRoute" debe devolver null. Por ejemplo, vea el código siguiente

      ```csharp
    public void GetConfigurationRoute(out string actionName,
                out string controllerName,
                out RouteValueDictionary routeValues)
    {
        actionName = "Configure";
        controllerName = "PaymentAuthorizeNet";
        routeValues = new RouteValueDictionary()
        {
            { "Namespaces", "Nop.Plugin.Payments.AuthorizeNet.Controllers" },
            { "area", null }
        };
    }
    ```

- (optional)Si necesita agregar alguna ruta personalizada, entonces cree el archivo  `RouteProvider.cs`Informa al sistema nopCommerce sobre las rutas de los complementos. Por ejemplo, la siguiente clase RouteProvider agrega una nueva ruta a la que se puede acceder abriendo su navegador web y navegando a la URL `http://www.yourStore.com/Plugins/PaymentPayPalStandard/PDTHandler` URL (used by PayPal plugin):

    ```csharp
    public partial class RouteProvider : IRouteProvider
    {
        public void RegisterRoutes(RouteCollection routes)
        {
             routes.MapRoute("Plugin.Payments.PayPalStandard.PDTHandler",
                 "Plugins/PaymentPayPalStandard/PDTHandler",
                 new { controller = "PaymentPayPalStandard", action = "PDTHandler" },
                 new[] { "Nop.Plugin.Payments.PayPalStandard.Controllers"  }
            );
        }

        public int Priority
        {
            get
            {
                return 0;
            }
        }
    }
    ```

    Una vez que haya instalado su plugin y agregado el método de configuración, encontrará un enlace para configurar su plugin en Admin → Configuración → Plugins.

## Handling "Install" and "Uninstall" methods

Este paso es opcional. Algunos plugin
s pueden requerir lógica adicional durante la instalación del plugin. Por ejemplo, un complemento puede insertar nuevos recursos de configuración regional. Por lo tanto, abra la implementación de IPlugiMn (en la mayoría de los casos se derivará de la clase BasePlugin) e invalide los métodos siguientes:

- Instalar. Este método se invocará durante la instalación de plugin. Puede inicializar cualquier configuración aquí, insertar nuevos recursos de configuración regional o crear algunas tablas de base de datos nuevas (si es necesario).
- Desinstalar. Este método se invocará durante la desinstalación de plugin.




> [!IMPORTANT]
> 
> Si invalida uno de estos métodos, no oculte su implementación base.

Por ejemplo, la estructura del proyecto de Authorize.NET plugin se parece a la imagen de abajo



```csharp
public override void Install()
{
    var settings = new AuthorizeNetPaymentSettings()
    {
        UseSandbox = true,
        TransactMode = TransactMode.Authorize,
        TransactionKey = "123",
        LoginId = "456"
    };
    _settingService.SaveSetting(settings);
    base.Install();
}
```

> [!TIP]
>
> La lista de complementos instalados se encuentra en `\App_Data\InstalledPlugins.txt`. La lista se crea durante la instalación.

## Actualizar nopCommerce puede romper los complementos

Algunos complementos pueden quedar desactualizados y ya no funcionan con la versión más reciente de nopCommerce. Si tiene problemas después de actualizar a la versión más reciente, elimine el complemento y visite el sitio web oficial de nopCommerce para ver si hay una versión más nueva disponible. Muchos autores de complementos actualizarán sus complementos para adaptarse a la versión más reciente, sin embargo, algunos no lo harán y su complemento se volverá obsoleto con las mejoras en nopCommerce. Pero en la mayoría de los casos, simplemente puede abrir un archivo `plugin.json` apropiado y actualizar el campo **SupportedVersions**.

## Conclusión

Con suerte, esto lo ayudará a comenzar con nopCommerce y lo preparará para crear complementos más elaborados .