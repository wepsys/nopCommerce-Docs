---
title: Currencies
uid: en/getting-started/configure-payments/advanced-configuration/currencies
author: git.AndreiMaz
contributors: git.exileDev, git.ivkadp, git.mariannk
---

# Monedas

En nopCommerce, se utiliza la **moneda de la tienda primaria**. La moneda de la tienda principal es la moneda contra la cual se configurarán todas las demás monedas permitidas. Aunque nopCommerce permite tener varias monedas para mostrar los precios de sus productos, la moneda principal se utiliza para las transacciones de pago con pasarelas de pago en línea.

Si utiliza una pasarela de pago en línea (como PayPal), el importe se envía a la pasarela de pago y será el precio que ingresó en la moneda de la tienda principal.

La moneda de la tienda principal solo la usan los administradores de la tienda. Se utiliza para fijar los precios de los productos y no tiene que ser el mismo que las monedas publicadas.

Si solo tiene una moneda publicada, la tienda no mostrará un selector de divisas ni ningún símbolo de moneda con precios. Si se publica más de una moneda, todos los precios se marcan con la moneda seleccionada actualmente. nopCommerce recomienda eliminar cualquier moneda que no sea necesaria.

nopCommerce utiliza un **tipo de cambio**  para calcular los importes de las monedas publicadas. El tipo de cambio se introduce cuando se añade o edita una moneda. Alternativamente, puede utilizar un servicio de tipo de cambio en tiempo real para calcular el importe, y el precio del producto se multiplica por el tipo de cambio proporcionado.

Los tipos de cambio fluctúan a diario. Por lo tanto, puede editar el tipo de cambio tan a menudo como lo necesite para mantenerse al día. Las transacciones reales solo se gestionan en la moneda principal de tu tienda. En las transacciones con tarjeta de crédito, los bancos generalmente realizarán intercambios automáticamente en función de los valores de moneda más actuales.

Para definir la configuración de la moneda, vaya a **Configuración > Monedas**.

![Monedas](_static/monedas/monedas1.png)

En la lista desplegable **Proveedor de tipo de cambio actual**,  seleccione el proveedor de tipo de cambio que se utilizará para obtener tasas de vida.

> [!NOTA]
>
> Por defecto en nopCommerce sólo hay un proveedor de tipo de cambio disponible - ECB. Para obtener tipos de cambio en vivo de ECB debe seleccionar EUR como moneda de tipo de cambio principal.

Marque la casilla de verificación **Actualización automática activada**  para permitir la recepción de una actualización automática de los tipos de cambio cada hora.

Haga clic en **Guardar**.

> [!NOTA]
>
> De forma predeterminada, todos los tipos de cambio se actualizan una vez por hora. Puede modificar la configuración de la actualización de los tipos de cambio en  **Sistema > Programar tareas**, seleccione  **Actualizar tipos de cambio de divisa**.

![Tarea de programación](_static/currencies/tasks.jpg)
# Añadir una nueva moneda

Haga clic en el botón Agregar nuevo.

![monedas3](_static/monedas/monedas3.png)

Defina la configuración de moneda:

* Moneda  **Nombre**.
* **Código de divisa**. Para obtener una lista de códigos de divisa, vaya a: https://en.wikipedia.org/wiki/ISO_4217
* Introduzca el cambio  **Tasa**  contra el tipo de cambio principal de la moneda.
* En la lista desplegable Mostrar configuración regional,seleccione  la configuración regional de visualización para los valores de moneda.
* Introduzca  **Formato personalizado**  que se aplicará a los valores de moneda. En este campo, puede especificar cualquier símbolo para la moneda que se muestra en el almacén público, el número de decimales, etc.
* En la lista desplegable **Limited to stores**  seleccione una tienda creada previamente. Deje el campo vacío en caso de que esta funcionalidad no sea necesaria.
> [!NOTA]
>
> Para utilizar esta funcionalidad, debe deshabilitar la siguiente configuración:  **Configuración del catálogo > Ignorar reglas de "límite por tienda" (en todo el sitio)**. Obtenga más información sobre la funcionalidad de varias tiendas [aquí](xref:en/getting-started/advanced-configuration/multi-store).

* En la lista desplegable **Tipo de redondeo**  elija uno de los tipos de redondeo:
* * Redondeo predeterminado*
* *Redondeo con intervalos de 0.05 (0.06 ronda a 0.10)*
* *Redondeo hacia abajo con intervalos de 0.05 (0.06 ronda a 0.05)*
* *Redondeo con 0.10 intervalos (1.05 ronda a 1.10)*
* *Redondeo hacia abajo con 0.10 intervalos (1.05 ronda a 1.00)*
* *Redondeo con intervalos de 0.50*
* *Redondeo con 1.00 intervalos (1.01-1.49 ronda a 1.00, 1.50-1.99 ronda a 2.00)*
* *Redondeo con 1.00 intervalos (1.01–1.99 ronda a 2.00)*

* Seleccione la casilla de verificación **Publicado**,  para permitir que esta moneda sea visible y seleccionada por los visitantes en su tienda. nopCommerce es compatible con una pantalla de precios multidivisa. Si tiene varias monedas publicadas, los clientes podrán seleccionar la moneda que desean.
* En el campo **Mostrar pedido**, introduzca el orden de visualización de esta moneda. Un valor de 1 representa la parte superior de la lista.

Haga clic en **Guardar**.
# Obtener tarifas en vivo

Haga clic en el botón Obtener tasas en vivo en la parte superior derecha de la ventana *Monedas*.  El panel se expande en la parte inferior de la página de la siguiente manera:

![Tipos de cambio envivo](_static/monedas/live-rates.jpg)

Haga clic en **Aplicar todo**  aquí o aplique manualmente nuevas tarifas para todas las monedas necesarias usando el botón **Aplicar tasa**.  
# Tutoriales

* [Gestión de monedas en nopCommerce](https://www.youtube.com/watch?v=2nzVxGyc5-M)

