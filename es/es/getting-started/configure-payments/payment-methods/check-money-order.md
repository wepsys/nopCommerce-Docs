---
title: Check/money order
uid: en/getting-started/configure-payments/payment-methods/check-money-order
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# Cheque/giro postal

Las agencias gubernamentales o las grandes empresas suelen utilizar cheques/giros postales. En lugar de pagar directamente a través de su sitio, los compradores le solicitarán que les envíe una **Orden de compra (PO)** y le devolverán el pago. La mayor parte del procesamiento de pedidos se realiza fuera del software.

Para configurar este método de pago, vaya a **Configuration → Payment methods**. Encuentra el **Check/money order (Payments.CheckMoneyOrder)** lista de métodos de pago:

![List](_static/check-money-order/list.jpg)

## Activar el método, editar su nombre y mostrar el orden

Puede editar el nombre del método de pago que se mostrará a los clientes en la tienda pública o su orden de exhibición. Para hacer esto, haga clic en el botón **Editar** en la fila del complemento en la página de lista de métodos de pago. Podrá ingresar **Nombre descriptivo** y **Orden de visualización**. En esta fila también puede activar el complemento o desactivarlo mediante el campo **Está activo**. Haga clic en el botón **Actualizar**. Se guardarán sus cambios.

## Configurar el método de pago

En **Configuración → Métodos de pago**, busque el método de pago **Cheque/giro postal (Payments.CheckMoneyOrder)** y haga clic en el botón **Configurar**. Aparecerá la ventana *Configurar - Cheque / giro postal*, de la siguiente manera:
![orden de compra](_static/check-money-order/purchaseorder.png)

Configure el método de pago de la siguiente manera:

* En el campo **Descripción** ingrese la información que se mostrará a los clientes durante el pago.
* Defina la **tarifa adicional** por usar este método.
* En la **Tarifa adicional. Usar porcentaje** campo define si se aplica una tarifa adicional porcentual al total del pedido. Si no está habilitado, se usa un valor fijo.
* El campo **Producto que se puede enviar es obligatorio** indica si se requieren productos que se pueden enviar para mostrar este método de pago durante el pago.

Clic en Guardar**.

## Límite a tiendas y roles de clientes

Puede limitar cualquier método de pago a la tienda y al rol del cliente. Esto significa que el método estará disponible solo para determinadas tiendas o roles de clientes. Puede hacerlo desde la página *lista de complementos*.

1. Vaya a **Configuración → Complementos locales**. Busque el complemento que desea limitar. En nuestro caso es **Cheque/giro postal**. Para encontrarlo más rápido, use el panel *Buscar* en la parte superior de la página y busque por **Nombre del complemento** o por **Grupo** usando la opción *Métodos de pago*.

![Plugins](_static/check-money-order/plugin.jpg)

1. Haga clic en el botón **Editar** y se mostrará la ventana *Editar detalles del complemento*, de la siguiente manera:

![Plugins](_static/check-money-order/edit.jpg)

2. Puede configurar los siguientes límites:

* En el campo **Limitado a roles de cliente**, elija uno o varios roles de cliente, es decir, administradores, proveedores, invitados, que podrán utilizar este complemento. Si no necesita esta opción, deje este campo vacío.

> [!IMPORTANT]
> Para utilizar esta funcionalidad, debe deshabilitar la siguiente configuración: **Configuración del catálogo → Ignorar las reglas de ACL (en todo el sitio)**. Leer más sobre la lista de control de acceso [aquí] (xref:en/running-your-store/customer-management/access-control-list).

* Utilice la opción **Limitado a tiendas** para limitar este complemento a una determinada tienda. Si tiene varias tiendas, elija una o varias de la lista. Si no usa esta opción, deje este campo vacío.

> [!IMPORTANT]
> Para utilizar esta funcionalidad, debe desactivar la siguiente configuración: **Configuración del catálogo → Ignorar las reglas de "límite por tienda" (en todo el sitio)**. Más información sobre la funcionalidad de varias tiendas [aquí](xref:en/getting-started/advanced-configuration/multi-store).

Click **guardar**.
