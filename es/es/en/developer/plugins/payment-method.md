---
title: How to code my own payment method
uid: en/developer/plugins/payment-method
author: git.AndreiMaz
contributors: git.Sandeep911, git.exileDev, git.DmitriyKulagin
---

# Cómo codificar mi propio método de pago

Los métodos de pago se implementan como complementos en nopCommerce. Le recomendamos que lea [Cómo escribir un complemento para nopCommerce 4.30](xref:en/developer/plugins/how-to-write-plugin-4.30) antes de comenzar a codificar un nuevo método de pago. Le explicará cuáles son los pasos necesarios para crear un complemento.

Entonces, en realidad, un método de pago es un complemento ordinario que implementa una interfaz IPaymentMethod (espacio de nombres Nop.Services.Payments). Como ya adivinó, la interfaz IPaymentMethod se utiliza para crear complementos de métodos de pago. Contiene algunos métodos que son específicos solo para métodos de pago como ProcessPayment () o GetAdditionalHandlingFee (). Así que agregue un nuevo proyecto de complemento de pago (biblioteca de clases) a la solución y comencemos.

## Controladores, vistas, modelos

Lo primero que debe hacer es crear un controlador. Este controlador es responsable de responder a las solicitudes realizadas contra un sitio web ASP.NET MVC.

1. Al implementar un nuevo método de pago, este controlador debe derivarse de una clase abstracta **BasePaymentController** especial.

1. Luego, implemente los métodos de acción **Configurar** utilizados para la configuración del complemento (por el propietario de una tienda en el área de administración). Este método y una vista adecuada definirán cómo el propietario de una tienda ve las opciones de configuración en el panel de administración (Sistema → Configuración → Métodos de pago).

## Componente de vista pública.GetPublicViewComponent

Luego, debe crear un componente de vista para mostrar el complemento en la tienda pública. Este componente de vista y una vista adecuada definirán cómo sus clientes verán la página de información de pago durante el pago. Primero, creemos una clase de componente de vista. Debe colocarse en la carpeta/Componentes. Mira cómo se hace con el complemento PayPalStandard:

```csharp
[ViewComponent(Name = "PaymentPayPalStandard")]
public class PaymentPayPalStandardViewComponent : NopViewComponent
{
    public IViewComponentResult Invoke()
    {
        return View("~/Plugins/Payments.PayPalStandard/Views/PaymentInfo.cshtml");
    }
}
```

El método de invocación devuelve una vista de PaymentInfo adecuada desde la carpeta */Views* de su complemento. Tenga en cuenta que usamos nuestra clase NopViewComponent personalizada como clase base en lugar de ViewComponent incorporado existente.

Luego, creemos la vista PaymentInfo que muestra la información de pago. Para el complemento PayPalStandard, esta vista es bastante simple. Allí solo mostramos texto que dice que un cliente será redirigido a la página de pago. Pero es posible crear un componente de vista más complejo si es necesario. Por ejemplo, si desea recopilar la información del cliente en la página de información de pago, mire cómo ya se hace en el complemento de pago PayPalDirect.

## Procesando pago

Ahora necesita crear una clase que implemente la interfaz **IPaymentMethod**. Esta es la clase que hará todo el trabajo real de comunicarse con su pasarela de pago. Cuando alguien crea un pedido, se llamará a los métodos **ProcessPayment** o **PostProcessPayment** de su clase. Así es como se define la clase CheckMoneyOrderPaymentProcessor (método de pago "CheckMoneyOrder"):

```csharp
public class CheckMoneyOrderPaymentProcessor : BasePlugin, IPaymentMethod
```

**La interfaz IPaymentMethod** tiene varios métodos y propiedades necesarios para implementar.

- **ValidatePaymentForm**  se utiliza en la tienda pública para validar la entrada del cliente. Devuelve una lista de advertencias (por ejemplo, un cliente no ha introducido el nombre de su tarjeta de crédito). Si su método de pago no pide al cliente que introduzca información adicional, ValidatePaymentForm debe devolver una lista vacía:



    ```csharp
    public IList<string> ValidatePaymentForm(IFormCollection form)
    {
        return new List<string>();
    }
    ```

- El **método GetPaymentInfo** se utiliza en el almacén público para analizar la entrada del cliente, como la información de la tarjeta de crédito. Este método devuelve un objeto ProcessPaymentRequest con información de cliente analizada (por ejemplo, información de tarjeta de crédito). Si su método de pago no pide al cliente que introduzca información adicional, GetPaymentInfo devolverá un objeto ProcessPaymentRequest vacío:



    ```csharp
    public ProcessPaymentRequest GetPaymentInfo(IFormCollection form)
    {
        return new ProcessPaymentRequest();
    }
    ```

- **ProcessPayment**. Este método siempre se invoca justo antes de que un cliente realice un pedido. Utilícelo cuando necesite procesar un pago antes de que un pedido se almacene en la base de datos. Por ejemplo, capture o autorice la tarjeta de crédito. Por lo general, este método se utiliza cuando un cliente no es redirigido a un sitio de terceros para completar un pago y todos los pagos se manejan en su sitio (por ejemplo, PayPal Direct).
- **PostProcessPayment**. Este método se invoca justo después de que un cliente realiza un pedido. Por lo general, este método se utiliza cuando necesita redirigir a un cliente a un sitio de terceros para completar un pago (por ejemplo, PayPal Standard).
- **HidePaymentMethod**. Puedes poner cualquier lógica aquí. Por ejemplo, oculte este método de pago si todos los productos del carrito se pueden descargar. O ocultar este método de pago si el cliente actual es de cierto país
- **GetAdditionalHandlingFee**. Puede devolver cualquier cargo de manipulación adicional que se agregará al total de un pedido.
- **Captura**. Algunas pasarelas de pago te permiten autorizar pagos antes de que se capturen. Permite a los propietarios de la tienda revisar los detalles del pedido antes de que el pago se realice realmente. En este caso, solo autoriza un pago en el método **ProcessPayment*
-  o  PostProcessPayment  (descrito anteriormente) y, a continuación, simplemente debe capturarlo. En este caso, un botón **Capturar**  estará visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que un pedido debe estar ya autorizado y  **SupportCapture**  propiedad debe devolver  **true**.
- **Reembolso**. Este método le permite hacer un reembolso. En este caso, un botón **Reembolso**  estará visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que se debe pagar un pedido y  **SupportRefund**  o  **SupportPartiallyRefund**  propiedad debe devolver  **true**.
- **Vacío**. Este método le permite anular un pago autorizado pero no capturado. En este caso, un botón **Void**  será visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que se debe autorizar un pedido y  **SupportVoid**  propiedad debe devolver  **true**.
- **ProcessRecurringPayment**. Utilice este método para procesar pagos recurrentes.
- **CancelRecurringPayment**. Utilice este método para cancelar pagos recurrentes.
- **CanRePostProcessPayment**. Por lo general, este método se utiliza cuando redirige a un cliente a un sitio de terceros para completar un pago. Si el pago de terceros falla, esta opción permitirá a los clientes intentar el pedido de nuevo más tarde sin realizar un nuevo pedido.  **CanRePostProcessPayment**  debe devolver  **true**  para habilitar esta característica.
- **GetConfigurationPageUrl**. Como recuerda, creamos un controlador en el paso anterior. Este método debe devolver una dirección URL de su Configure método. Por ejemplo:



    ```csharp
    public override string GetConfigurationPageUrl()
    {
        return $"{_webHelper.GetStoreLocation()}Admin/PaymentCheckMoneyOrder/Configure";
    }
    ```

- **GetPublicViewComponent**. Este método debe devolver el nombre del componente de vista que se utiliza para mostrar información pública para los clientes. Hemos creado un componente de vista adecuado en el paso anterior. Por ejemplo,

:

    ```csharp
    public string GetPublicViewComponent()
    {
        viewComponentName = "CheckMoneyOrder";
    }
    ```

- **SupportCapture, SupportPartiallyRefund, SupportRefund, SupportVoid**. Estas propiedades indican si se admiten los métodos adecuados de su método de pago.
- **RecurringPaymentType**. Esta propiedad indica si se admiten pagos recurrentes.
- **PaymentMethodType**. Esta propiedad indica el tipo de método de pago. Actualmente hay tres tipos.  **Estándar**  utilizado por los métodos de pago cuando un cliente no es redirigido a un sitio de terceros. **La redirección**  se utiliza cuando un cliente es redirigido a un sitio de terceros. Y  **Button**  es similar a los métodos de pago de redirección.  La única diferencia se utiliza que se muestra como un botón en la página del carro de la compra (por ejemplo, Google Checkout).
- **SkipPaymentInfo**. Indica si debemos mostrar una página de información de pago para este plugin.
- **PaymentMethodDescription**. Esta propiedad obtiene una descripción del método de pago que se mostrará en las páginas de pago en la tienda pública

# Conclusión

Esperemos que esto le ayudará a empezar a agregar un nuevo método de pago.


