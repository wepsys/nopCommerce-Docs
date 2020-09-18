---
title: How to code my own shipping rate computation method
uid: en/developer/plugins/shipping-plugin
author: git.AndreiMaz
contributors: git.exileDev
---

# Cómo codificar mi propio método de cálculo de la tarifa de envío

Si los clientes tienen algunos productos que se pueden enviar, pueden elegir una opción de envío durante el proceso de pago. Estas opciones de envío se devuelven de los métodos de cálculo de la tarifa de envío (como UPS, USPS, FedEx, etc.). Los métodos de cálculo de la tasa de envío se implementan como plugins en nopCommerce. Le recomendamos que lea [Cómo escribir un plugin para nopCommerce 4.30](xref:en/developer/plugins/how-to-write-plugin-4.30) antes de comenzar acodificar un nuevo método de cálculo de la tasa de envío. El artículo le explicará los pasos necesarios para crear un plugin. Así que en realidad un método de cálculo de la tasa de envío es un complemento ordinario que implementa una interfaz **IShippingRateComputationMethod**  (espacio de nombres Nop.Services.Shipping). Así que agregue un nuevo proyecto de plugin de envío (biblioteca de clases) a la solución y comencemos.

## Controladores, vistas, modelos

Agregue un controlador y un método de acción /*Configure** adecuado y una vista. Estos definirán cómo el propietario de una tienda ve las opciones de configuración en el panel de administración (Sistema , Configuración, Envío y Proveedores de envío). Este artículo no explica cómo configurar plugins, pero puede encontrar más información al respecto [aquí](xref:en/getting-started/configure-shipping/shipping-providers/index).

![envío-plugin_1](_static/shipping-plugin/shipping-plugin_1.png)

Una vez completado este paso, puede empezar a agregar la lógica de negocios necesaria para obtener las opciones de envío.

## Obtener opciones de envío

Ahora necesita crear una clase que implemente la interfaz IShippingRateComputationMethod.*  . Esta es la clase que hará todo el trabajo real. Cuando nopCommerce calcula los totales de envío o necesita obtener una lista de opciones de envío disponibles, se llamará a los métodos **GetShippingOptions**  o  GetFixedRate de su clase. Así es como se define la clase UPSComputationMethod ("método UPS"):



```csharp
public class UPSComputationMethod : BasePlugin, IShippingRateComputationMethod
```

**IShippingRateComputationMethod** interface has several methods and properties which are required to implement.

- **ShippingRateComputationMethodType**. Esta propiedad indica cómo funciona el cálculo de la tarifa de envío. Puede ser  **Offline**  o  **Realtime**. **Offline**  plugins no utilizan sitios de terceros para obtener las tarifas (ejemplos de tales métodos son "Fijo o por peso"). Estos plugins obtienen toda la información requerida de las bases de datos locales.  **Realtime**  plugins utilizan sitios de terceros para obtener las tarifas (por ejemplo, UPS).
- **GetShippingOptions**. Este método siempre se invoca cuando un cliente elige una opción de envío durante el proceso de pago. Este método devuelve  **GetShippingOptionResponse**  que contiene una lista de objetos **ShippingOption**.  Cada objeto **ShippingOption**  contiene información sobre ciertas opciones de envío, como el nombre de la opción (por ejemplo, "Por tierra"), su tarifa (por ejemplo, 10 USD) y otra información. Ponga toda su lógica aquí (obtenga las tarifas de su base de datos o úselas de un sitio de terceros como UPS).
- **GetFixedRate**. Como ya sabe  **GetShippingOptions**  se utiliza para obtener opciones de envío durante el pago (en la página "Seleccionar método de envío"). Pero a veces necesitamos conocer una tarifa de envío antes de que se elija una opción de envío (por ejemplo, en la página del carro de la compra). En este caso, puede devolver una tarifa fija. Por ejemplo, el método de cálculo de la tarifa de envío solo proporciona una opción de envío y no hay necesidad de esperar hasta que el cliente lo elija en la página "Seleccionar método de envío". La devolución será  null,si no se admiten las tarifas fijas. En este caso, los clientes verán el siguiente mensaje junto a "Total de envío" en el carro de la compra: "Calculado durante el pago".
- **GetConfigurationPageUrl**. Como recuerda, creamos un controlador en el paso anterior. Este método debe devolver una dirección URL de su Configure método. Por ejemplo:



```csharp
public override string GetConfigurationPageUrl()
{
    return $"{_webHelper.GetStoreLocation()}Admin/FixedOrByWeight/Configure";
}
```

## Conclusión

Esperemos que esto le ayudará a empezar con la adición de un nuevo método de cálculo de la tarifa de envío.


