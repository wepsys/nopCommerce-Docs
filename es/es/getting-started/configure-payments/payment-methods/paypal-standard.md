---
title: PayPal Standard
uid: en/getting-started/configure-payments/payment-methods/paypal-standard
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# Estándar de PayPal

PayPal Standard es la forma más fácil de aceptar de forma segura pagos con tarjeta de crédito y PayPal en línea.

## Activa el método, edita su nombre y muestra el orden

Puede editar el nombre del método de pago que se mostrará a los clientes en la tienda pública o su orden de exhibición. Para hacer esto, haga clic en el botón **Editar** en la fila del plugin en la página de lista de métodos de pago. Podrá ingresar **Nombre descriptivo** y **Orden de visualización**. En esta fila también puede activar el plugin o desactivarlo mediante el campo **Está activo**. Haga clic en el botón **Actualizar**. Se guardarán sus cambios.

## Configurar el método de pago

Para utilizar el plugin **Estándar de PayPal** como método de pago, siga estos pasos:

1. Registre una cuenta comercial en www.paypal.com. Siguiendo el enlace [https://www.paypal.com/bizsignup/](https://www.paypal.com/bizsignup/). Luego, complete la información sobre usted y su negocio:

    ![paso1](_static/paypal-standard/signUp1step.png)

    > [!NOTE]
    >
    > Si ya tiene una cuenta, será redirigido a la autorización.

    ![paso2](_static/paypal-standard/signUp2step.png)

    ![paso3](_static/paypal-standard/signUp3step.png)

    ![paso4](_static/paypal-standard/signUp4step.png)

    ![paso5](_static/paypal-standard/signUp5step.png)

1. En la barra de navegación superior, haga clic en el ícono **Configuración** ![Configuración](_static/paypal-standard/settings_icon.png)

1. Seleccione **Pagos del sitio web** en el panel izquierdo y haga clic en **Actualizar** en la línea **Preferencias del sitio web**.

    ![websitepayments] (_static/paypal-standard/websitepaymentsppal.png)
1. En la sección **Devolución automática para pagos en el sitio web**, configure el interruptor en **Activado.** Como **URL de devolución** ingrese la URL de su sitio, que recibirá las transacciones de identificación enviadas por PayPal después del cliente. pago.

    ![autoreturnURLPP](_static/paypal-standard/autoreturnURLPP.png)
1. En la sección **Transferencia de datos de pago**, coloque el interruptor en **Activado** y copie **Token de identidad.**

    ![PDTtoken](_static/paypal-standard/PDTtoken.png)
1. Para configurar el plugin en el panel de administración de nopCommerce, vaya a **Configuración → Métodos de pago**. En la línea **Estándar de PayPal**, haga clic en **Confige**.

![nopconfig](_static/paypal-standard/nopConfigPP.png)

1. En el campo **Correo electrónico comercial**, ingrese un correo electrónico especificado al registrar una cuenta comercial en paypal.com.

1. En el campo **PDT Identity Token** ingrese el **Identity Token** copiado de la cláusula # 5.

1. Haga clic en **Guardar**.

Para la activación de **IPN** (Notificación de pago instantánea):

1. Seleccione **Notificaciones** en el panel izquierdo y haga clic en **Actualizar en la línea Notificaciones de pago instantáneo**.

![notificaciones](_static/paypal-standard/NotificationsPP.png)

1. Familiarícese con la información sobre **IPN** y haga clic en **Elegir configuración de IPN**.

![ChooseIPN](_static/paypal-standard/chooseIPNSettings.png)

1. Seleccione **Recibir mensajes IPN (habilitado)**. Como **URL de notificación**, ingrese la URL de su controlador de IPN.

![editIPN](_static/paypal-standard/editIPN.png)

1. Haga clic en **Guardar.** Debería recibir un mensaje de que ha activado correctamente la IPN.

> [!NOTE]
>
> Notificación de pago instantánea (IPN) es el servicio de mensajes de PayPal que envía una notificación cuando una transacción se ve afectada. Una vez que se integra IPN, los vendedores pueden automatizar su back office para que no tengan que esperar a que lleguen los pagos para activar el cumplimiento del pedido.

## Límite a tiendas y roles de clientes

Puede limitar cualquier método de pago a la tienda y al rol del cliente. Esto significa que el método estará disponible solo para determinadas tiendas o roles de clientes. Puede hacerlo desde la página *lista de plugins*.

1. Vaya a **Configuración → plugins locales**. Busque el plugin que desea limitar. En nuestro caso es **Estándar de PayPal**. Para encontrarlo más rápido, use el panel *Buscar* en la parte superior de la página y busque por **Nombre del plugin** o por **Grupo** usando la opción *Métodos de pago*.

![plugins](_static/paypal-standard/plugin.jpg)

1. Haga clic en el botón **Editar** y se mostrará la ventana *Editar detalles del plugin*, de la siguiente manera:

![plugins](_static/paypal-standard/edit.jpg)

2. Puede configurar los siguientes límites:

* En el campo **Limitado a roles de cliente**, elija uno o varios roles de cliente, es decir, administradores, proveedores, invitados, que podrán utilizar este plugin. Si no necesita esta opción, deje este campo vacío.

> [!important]
> Para utilizar esta funcionalidad, debe deshabilitar la siguiente configuración: **Configuración del catálogo → Ignorar las reglas de ACL (en todo el sitio)**. Lea más sobre la lista de control de acceso [aquí](xref:en/running-your-store/customer-management/access-control-list).

* Utilice la opción **Limitado a tiendas** para limitar este plugin a una determinada tienda. Si tiene varias tiendas, elija una o varias de la lista. Si no usa esta opción, deje este campo vacío.

> [!important]
> Para utilizar esta funcionalidad, debe desactivar la siguiente configuración: **Configuración del catálogo → Ignorar las reglas de "límite por tienda" (en todo el sitio)**. Leer más sobre multi-st