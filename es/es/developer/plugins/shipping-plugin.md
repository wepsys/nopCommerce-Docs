---
title: How to code my own shipping rate computation method
uid: en/developer/plugins/shipping-plugin
author: git.AndreiMaz
contributors: git.exileDev
---

# Cómo codificar mi propio método de cálculo de tarifas de envío

Si los clientes tienen algunos productos que se pueden enviar, pueden elegir una opción de envío durante el pago. Estas opciones de envío se devuelven a partir de métodos de cálculo de tarifas de envío (como UPS, USPS, FedEx, etc.). Los métodos de cálculo de tarifas de envío se implementan como complementos en nopCommerce. Le recomendamos que lea [Cómo escribir un complemento para nopCommerce 4.30](xref:en/developer/plugins/how-to-write-plugin-4.30) antes de comenzar a codificar un nuevo método de cálculo de tarifas de envío. El artículo le explicará los pasos necesarios para crear un complemento. Entonces, en realidad, un método de cálculo de tarifas de envío es un complemento ordinario que implementa una interfaz **IShippingRateComputationMethod** (espacio de nombres Nop.Services.Shipping). Así que agregue un nuevo proyecto de complemento de envío (biblioteca de clases) a la solución y comencemos.

## Controladores, vistas, modelos

Agregue un controlador y un método de acción **Configurar** apropiado y una vista. Estos definirán cómo el propietario de una tienda ve las opciones de configuración en el panel de administración (Sistema → Configuración → Envío → Proveedores de envío). Este artículo no explica cómo configurar los complementos, pero puede encontrar más información al respecto [aquí](xref:en/Getting-started/configure-shipping/shipping-Suppliers/index).

![shipping-plugin_1](_static/shipping-plugin/shipping-plugin_1.png)

Una vez que haya completado este paso, puede comenzar a agregar la lógica comercial requerida para obtener opciones de envío.

## Obtener opciones de envío

Ahora necesita crear una clase que implemente la interfaz **IShippingRateComputationMethod**. Esta es la clase que hará todo el trabajo real. Cuando nopCommerce calcula los totales de envío o necesita obtener una lista de las opciones de envío disponibles, se llamarán a los métodos **GetShippingOptions** o **GetFixedRate** de su clase. Así es como se define la clase UPSComputationMethod (método"UPS"):

```csharp
public class UPSComputationMethod : BasePlugin, IShippingRateComputationMethod
```

La interfaz **IShippingRateComputationMethod** tiene varios métodos y propiedades que se requieren para implementar.

- **ShippingRateComputationMethodType**. Esta propiedad indica cómo funciona el cálculo de la tarifa de envío. Puede ser **sin conexión** o **en tiempo real**. Los complementos **sin conexión** no utilizan sitios de terceros para obtener las tarifas (ejemplos de tales métodos son "Fijos o por peso"). Estos complementos obtienen toda la información necesaria de las bases de datos locales. Los complementos **en tiempo real** utilizan sitios de terceros para obtener las tarifas (por ejemplo, UPS).
- **GetShippingOptions**. Este método siempre se invoca cuando un cliente elige una opción de envío durante el pago. Este método devuelve **GetShippingOptionResponse** que contiene una lista de objetos **ShippingOption**. Cada objeto **ShippingOption** contiene información sobre determinadas opciones de envío, como el nombre de la opción (por ejemplo, "Por tierra"), su tarifa (por ejemplo, 10 USD) y otra información. Ponga toda su lógica aquí (obtenga las tarifas de su base de datos o solicítelas en un sitio de terceros como UPS).
- **GetFixedRate**. Como ya sabe, **GetShippingOptions** se utiliza para obtener opciones de envío durante el pago (en la página "Seleccionar método de envío"). Pero a veces necesitamos conocer una tarifa de envío antes de elegir una opción de envío (por ejemplo, en la página del carrito de compras). En este caso puede devolver una tarifa fija. Por ejemplo, su método de cálculo de la tarifa de envío proporciona solo una opción de envío y no es necesario esperar hasta que el cliente lo elija en la página "Seleccionar método de envío". La devolución será **nula**, si sus tarifas fijas no son compatibles. En este caso, los clientes verán el siguiente mensaje junto a "Total de envío" en el carrito de compras: "Calculado durante el pago".
- **GetConfigurationPageUrl**. Como recordará, creamos un controlador en el paso anterior. Este método debería devolver una URL de su método Configure. Por ejemplo:

```csharp
public override string GetConfigurationPageUrl()
{
    return $"{_webHelper.GetStoreLocation()}Admin/FixedOrByWeight/Configure";
}
```

## Conclusión

Con suerte, esto le ayudará a comenzar a agregar un nuevo método de cálculo de tarifas de envío.
