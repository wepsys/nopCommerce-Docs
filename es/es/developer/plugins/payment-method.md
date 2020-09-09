---
title: How to code my own payment method
uid: en/developer/plugins/payment-method
author: git.AndreiMaz
contributors: git.Sandeep911, git.exileDev, git.DmitriyKulagin
---

# Cómo codificar mi propio método de pago

Los métodos de pago se implementan como complementos en nopCommerce. Le recomendamos que lea [Cómo escribir un complemento para nopCommerce 4.30] (xref:en/developer/plugins/how-to-write-plugin-4.30) antes de comenzar a codificar un nuevo método de pago. Le explicará cuáles son los pasos necesarios para crear un complemento.

Entonces, en realidad, un método de pago es un complemento ordinario que implementa una interfaz IPaymentMethod (espacio de nombres Nop.Services.Payments). Como ya adivinó, la interfaz IPaymentMethod se utiliza para crear complementos de métodos de pago. Contiene algunos métodos que son específicos solo para métodos de pago como ProcessPayment () o GetAdditionalHandlingFee (). Así que agregue un nuevo proyecto de complemento de pago (biblioteca de clases) a la solución y comencemos.

## Controladores, vistas, modelos

Lo primero que debe hacer es crear un controlador. Este controlador es responsable de responder a las solicitudes realizadas en un sitio web ASP.NET MVC.

1. Al implementar un nuevo método de pago, este controlador debe derivarse de una clase abstracta **BasePaymentController** especial.

1. Luego implemente los métodos de acción **Configurar** utilizados para la configuración del complemento (por el propietario de una tienda en el área de administración). Este método y una vista adecuada definirán cómo el propietario de una tienda ve las opciones de configuración en el panel de administración (Sistema → Configuración → Métodos de pago).

## Componente de vista pública.GetPublicViewComponent

Luego, debe crear un componente de vista para mostrar el complemento en la tienda pública. Este componente de vista y una vista adecuada definirán cómo sus clientes verán la página de información de pago durante el pago. Primero, creemos una clase de componente de vista. Debe colocarse en la carpeta/Componentes. Mira cómo se hace para el complemento PayPalStandard:

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

El método de invocación devuelve una vista de PaymentInfo adecuada desde la carpeta * / Views * de su complemento. Tenga en cuenta que usamos nuestra clase personalizada NopViewComponent como clase base en lugar de ViewComponent incorporado existente.

Luego, creemos la vista PaymentInfo que muestra la información de pago. Para el complemento PayPalStandard, esta vista es bastante simple. Allí solo mostramos un texto que dice que un cliente será redirigido a la página de pago. Pero es posible crear un componente de vista más complejo si es necesario. Por ejemplo, si desea recopilar la información del cliente en la página de información de pago, mire cómo ya se hace en el complemento de pago PayPalDirect.

## Procesando pago

Ahora necesita crear una clase que implemente la interfaz **IPaymentMethod**. Esta es la clase que hará todo el trabajo real de comunicarse con su pasarela de pago. Cuando alguien crea un pedido, se llamará a los métodos **ProcessPayment** o **PostProcessPayment** de su clase. Así es como se define la clase CheckMoneyOrderPaymentProcessor (método de pago "CheckMoneyOrder"):
```csharp
public class CheckMoneyOrderPaymentProcessor : BasePlugin, IPaymentMethod
```

La interfaz **IPaymentMethod** tiene varios métodos y propiedades que se requieren para implementar.

- **ValidatePaymentForm** se utiliza en la tienda pública para validar la entrada del cliente. Devuelve una lista de advertencias (por ejemplo, un cliente no ingresó el nombre de su tarjeta de crédito). Si su método de pago no le pide al cliente que ingrese información adicional, ValidatePaymentForm debería devolver una lista vacía:
    ```csharp
    public IList<string> ValidatePaymentForm(IFormCollection form)
    {
        return new List<string>();
    }
    ```

- **GetPaymentInfo** El método se utiliza en la tienda pública para analizar la entrada del cliente, como la información de la tarjeta de crédito. Este método devuelve un objeto ProcessPaymentRequest con la entrada del cliente analizada (por ejemplo, información de la tarjeta de crédito). Si su método de pago no le pide al cliente que ingrese información adicional, GetPaymentInfo devolverá un objeto ProcessPaymentRequest vacío:

    ```csharp
    public ProcessPaymentRequest GetPaymentInfo(IFormCollection form)
    {
        return new ProcessPaymentRequest();
    }
    ```

- **Procesar pago**. Este método siempre se invoca justo antes de que un cliente realice un pedido. Úselo cuando necesite procesar un pago antes de que un pedido se almacene en la base de datos. Por ejemplo, capturar o autorizar tarjeta de crédito. Por lo general, este método se usa cuando un cliente no es redirigido a un sitio de terceros para completar un pago y todos los pagos se manejan en su sitio (por ejemplo, PayPal Direct).
- **PostProcessPayment**. Este método se invoca inmediatamente después de que un cliente realiza un pedido. Por lo general, este método se utiliza cuando necesita redirigir a un cliente a un sitio de terceros para completar un pago (por ejemplo, PayPal estándar).
- **HidePaymentMethod**. Puedes poner cualquier lógica aquí. Por ejemplo, oculte este método de pago si todos los productos del carrito se pueden descargar. O esconda este método de pago si el cliente actual es de cierto país
- **GetAdditionalHandlingFee**. Puede devolver cualquier tarifa de manejo adicional que se agregará al total del pedido.
- **Capturar**. Algunas pasarelas de pago le permiten autorizar pagos antes de que sean capturados. Permite a los propietarios de las tiendas revisar los detalles del pedido antes de que se realice el pago. En este caso, solo autoriza un pago en el método **ProcessPayment** o **PostProcessPayment** (descrito anteriormente), y luego simplemente capturalo. En este caso, un botón **Capturar** será visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que un pedido ya debería estar autorizado y la propiedad **SupportCapture** debería devolver **true**.
- **Reembolso**. Este método le permite realizar un reembolso. En este caso, un botón **Reembolso** será visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que se debe pagar un pedido y que la propiedad **SupportRefund** o **SupportPartiallyRefund** debe devolver **true**.
- **Nulo**. Este método le permite anular un pago autorizado pero no capturado. En este caso, un botón **Anular** será visible en la página de detalles del pedido en el área de administración. Tenga en cuenta que un pedido debe estar autorizado y la propiedad **SupportVoid** debe devolver **true**.
- **ProcessRecurringPayment**. Utilice este método para procesar pagos recurrentes.
- **Cancelar pago recurrente**. Utilice este método para cancelar pagos recurrentes.
- **CanRePostProcessPayment**. Por lo general, este método se usa cuando redirige a un cliente a un sitio de terceros para completar un pago. Si el pago de un tercero falla, esta opción permitirá a los clientes volver a intentar el pedido más tarde sin realizar un nuevo pedido. **CanRePostProcessPayment** debería devolver **true** para habilitar esta función.
- **GetConfigurationPageUrl**. Como recordará, creamos un controlador en el paso anterior. Este método debería devolver una URL de su método Configure. Por ejemplo:

    ```csharp
    public override string GetConfigurationPageUrl()
    {
        return $"{_webHelper.GetStoreLocation()}Admin/PaymentCheckMoneyOrder/Configure";
    }
    ```

- **GetPublicViewComponent**. Este método debe devolver el nombre del componente de vista que solía mostrar información pública a los clientes. Hemos creado un componente de vista apropiado en el paso anterior. Por ejemplo:
    ```csharp
    public string GetPublicViewComponent()
    {
        viewComponentName = "CheckMoneyOrder";
    }
    ```

- **SupportCapture, SupportPartiallyRefund, SupportRefund, SupportVoid**. Estas propiedades indican si se admiten los métodos adecuados de su método de pago.
- **RecurringPaymentType**. Esta propiedad indica si se admiten pagos recurrentes.
- **PaymentMethodType**. Esta propiedad indica el tipo de método de pago. Actualmente existen tres tipos. **Estándar** utilizado por los métodos de pago cuando un cliente no es redirigido a un sitio de terceros. **Redirección** se utiliza cuando un cliente es redirigido a un sitio de terceros. Y **Button** es similar a los métodos de pago **Redirection**. La única diferencia es que se muestra como un botón en la página del carrito de compras (por ejemplo, Google Checkout).
- **SkipPaymentInfo**. Indica si deberíamos mostrar una página de información de pago para este complemento.
- **PaymentMethodDescription**. Esta propiedad obtiene una descripción del método de pago que se mostrará en las páginas de pago en la tienda pública.

## Conclusión

Con suerte, esto le ayudará a comenzar a agregar un nuevo método de pago.
