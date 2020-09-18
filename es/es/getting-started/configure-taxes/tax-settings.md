---
title: Tax settings
uid: en/getting-started/configure-taxes/tax-settings
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Configuración de impuestos

Esta sección describe la configuración de impuestos de su tienda, por ejemplo, la definición de precios con o sin impuestos, la definición del tipo de visualización de impuestos y más.

Para administrar su configuración de impuestos, vaya a **Configuración → Configuración → Configuración de impuestos**.

![Configuración de impuestos](_static/tax-settings/tax-settings.jpg)

En primer lugar, defina la configuración impositiva **común**:
* De la lista desplegable **Impuesto basado en**, seleccione la opción requerida en la que se basa el impuesto, de la siguiente manera:
  * **Dirección de Envio**. Cuando se selecciona esta opción, el impuesto se basa en la dirección de facturación del cliente. Si se desconoce la dirección de facturación, se utiliza la dirección predeterminada (ingresada a continuación).
  * **Dirección de Envío**. Cuando se selecciona esta opción, el impuesto se basa en la dirección de envío del cliente. Si se desconoce la dirección de envío, se utiliza la dirección predeterminada (ingresada a continuación).
  * **Dirección predeterminada**. Cuando se selecciona esta opción, el impuesto se basa en la dirección predeterminada que se ingresa a continuación.
* Elija la **Categoría de impuestos predeterminada** para los productos. Se preseleccionará en la página *Agregar nuevo producto*.
* **Impuestos basados ​​en la dirección del punto de recogida** La casilla de verificación define si se debe utilizar una dirección de punto de recogida para el cálculo de impuestos cuando se elige el punto de recogida.
* Marque la casilla de verificación **Los precios incluyen impuestos** para indicar si los precios ingresados ​​incluyen impuestos.

Luego defina la **dirección fiscal predeterminada (utilizada para el cálculo de impuestos)**, de la siguiente manera:
* Seleccione **País**.
* Seleccione **Estado/provincia**.
* Defina **Condado/región**.
* Defina la **Ciudad**.
* Defina la **Dirección 1**.
* Ingrese **Código postal**.

En el panel **Visualización de impuestos** puede configurar cómo se mostrarán los impuestos a los clientes:
* Marque la casilla de verificación **Permitir que los clientes seleccionen el tipo de visualización de impuestos**, para indicar si los clientes pueden seleccionar el tipo de visualización de impuestos. Cuando se desmarca, se muestra la lista desplegable **Tipo de visualización de impuestos**:
  * **Sin impuestos**: seleccione para aplicar sin impuestos.
  * **Impuestos incluidos**: seleccione para aplicar impuestos incluidos.
* Marque la casilla de verificación **Mostrar sufijo de impuestos**, para mostrar el sufijo de impuestos (incl.Impuestos\excl.Impuestos).
* Marque la casilla de verificación **Mostrar todas las tasas impositivas aplicadas** para mostrar todas las tasas impositivas aplicadas en una línea separada en la página del carrito de compras.
* Marque la casilla de verificación **Ocultar impuestos cero** para ocultar el valor de impuestos cero en el resumen del pedido.
* Marque la casilla de verificación **Ocultar impuestos en el resumen del pedido** para ocultar el valor del impuesto en el resumen del pedido cuando los precios se muestran con impuestos incluidos.
* Marque la casilla de verificación **Forzar la exclusión de impuestos del subtotal del pedido**, para excluir siempre el impuesto del subtotal del pedido (irrelevante para el tipo de visualización de impuestos seleccionado). Esta casilla de verificación afecta solo a las páginas donde se muestran los totales de los pedidos.

En el panel *Envío*, marque la casilla de verificación **El envío está sujeto a impuestos** para indicar que el envío está sujeto a impuestos. A continuación, se muestran los siguientes campos:
* **El precio de envío incluye impuestos**: seleccione para indicar que el precio de envío incluye impuestos.
* **Categoría de impuestos sobre el envío**: seleccione la categoría de impuestos requerida para el cálculo del impuesto sobre el envío.

En el panel *Pago*, marque la casilla e verificación **La tarifa adicional del método de pago está sujeta a impuestos** para indicar que la tarifa adicional del método de pago está sujeta a impuestos. A continuación, se muestran las siguientes opciones:
* **La tarifa adicional del método de pago incluye impuestos**: seleccione para indicar que la tarifa adicional del método de pago está sujeta a impuestos.
* **Categoría de impuesto de tarifa adicional del método de pago**: de la lista desplegable, seleccione la categoría de impuesto requerida utilizada para el cálculo de impuesto de tarifa adicional del método de pago.

Luego configure el IVA en el panel *IVA*:
* Marque la casilla de verificación **IVA de la UE habilitado**, para indicar que el impuesto al valor agregado de la Unión Europea está habilitado. Cuando se selecciona esta opción, se solicitará a los clientes el *Número de IVA de la empresa* durante el registro o en la página de detalles de la cuenta del cliente. Este número de IVA se puede validar automáticamente a través de un servicio web, si la casilla de verificación **Usar servicio web** está marcada, o manualmente en la página de detalles del cliente en el área de administración por el propietario de la tienda.
* **País de su tienda**: en la lista desplegable, seleccione el país donde se encuentra su tienda.
* **Permitir exención de IVA**: marque esta casilla de verificación para eximir del IVA a los clientes registrados con IVA elegibles.
* **Suponga que el IVA siempre es válido**: marque esta casilla de verificación para omitir la validación del IVA. Los números de IVA ingresados ​​siempre serán válidos. Es responsabilidad del cliente proporcionar el número de IVA vigente.
* **Usar el servicio web:** marque esta casilla de verificación para usar el servicio web para validar los números de IVA.
* **Notificar al administrador cuando se envíe un nuevo número de IVA**: marque esta casilla de verificación para recibir una notificación por correo electrónico cuando se envíe un nuevo número de IVA.

> [!NOTE]
>
> Si el IVA está habilitado, se cobra 0% de impuestos a los envíos fuera de la UE y 0% a aquellos que han proporcionado un número de IVA validado y aprobado y están enviando dentro de la UE pero fuera del país de la tienda. Consulte un artículo para obtener más información sobre el IVA de la UE.

> [!TIP]
>
> Lea cómo configurar el IVA de la UE aquí: [Guía de configuración del IVA de la UE](xref:es/Getting-started/configure-tax/index#eu-vat-configuration-guide).

Clic en **Guardar**.

### Tutor(https://www.youtube.com/watch?v=8iF5nQvIoLs&feature=youtu.be)
