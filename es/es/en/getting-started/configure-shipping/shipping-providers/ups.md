---
title: UPS
uid: en/getting-started/configure-shipping/shipping-providers/ups
author: git.AndreiMaz
contributors: git.exileDev
---

# UPS

To access your account at UPS use a username, a password, and an **XML license number**, which you will be provided with after the registration process.

## Define the UPS Real Time Shipping Calculations

1. Create a UPS account by going to [https://www.ups.com/upsdeveloperkit?loc=en_US](https://www.ups.com/upsdeveloperkit?loc=en_US) to receive the following:
    * Username ID
    * Password
    * XML access license number

1. In nopCommerce admin area go to **Configuration → Shipping → Shipping providers**. 
 ![Shipping rate methods](_static/ups/shipping-rate-methods.jpg)
1. Enable this method, as follows:
    * In the UPS (United Postal Service) row, click the **Edit** button.
    * In the Is **active** column, check the checkmark.
    * Click **Update**. The *false* option becomes *true*.• UPS

Para acceder a su cuenta en UPS, utilice un nombre de usuario, una contraseña y un **número de licencia XML**, que se le proporcionará después del proceso de registro.

• Definir los cálculos de envío en tiempo real de UPS

1. Cree una cuenta UPS yendo a [https://www.ups.com/upsdeveloperkit?loc=en_US](https://www.ups.com/upsdeveloperkit?loc=en_US) para recibirlo siguiente:
* ID de nombre de usuario
* Contraseña
* Número de licencia de acceso XML

1. En el área de administración de nopCommerce vaya a  **Configuración > Envío > Proveedores de envío**.
! [Métodos de tarifa de envío](_static/ups/shipping-rate-methods.jpg)
1. Habilite este método, como se indica a continuación:
* En la fila UPS (United Postal Service), haga clic en el botón **Editar**.  
* En la columna Is **active**,  marque la marca de verificación.
* Haga clic en  **Actualizar**. La opción *false*  se convierte en  *true*.

1. Haga clic en  **Configurar**  junto a la opción UPS (United Parcel Service) de la lista.
Se muestra la ventana *Configurar – UPS (United Parcel Service)*,  como se indica a continuación: ![ Configurar página](_static/ups/ups-configure.jpg)

1. Introduzca la siguiente información obtenida del proveedor de UPS:
* Marque la casilla de verificación **Usar sandbox** para utilizar el entorno de prueba.
* Introduzca el  **Número de cuenta**  del proveedor de UPS.
* Introduzca la clave de acceso ***  obtenida del proveedor.
* Introduzca su  **Nombre de usuario** obtenido del proveedor.
* Introduzca la  **Contraseña**  obtenida del proveedor
* Seleccione su clasificación de cliente de UPS requerida, de la siguiente manera:
* Tarifas asociadas con el número de remitente
* Tarifas diarias
* Tarifas de venta al por menor
* Tarifas Regionales
* Tasas de lista general
* Tarifas de lista estándar
* Seleccione el ** Tipo de recogida UPS requerido**, de la siguiente manera:  
* Recogida diaria
* Contador de clientes
* Recogida de una sola vez
* On Call Air
* Centro de Cartas
* Centro de Servicio Aéreo
* Seleccione el **UPS Packaging Type** requerido, de la siguiente manera:
* Desconocido
* Carta
* Paquete suministrado por el cliente
* Tubo
* P A K
* Caja Exprés
* Caja de 10 kg
* Caja de 25 kg
* Paleta
* Caja Express Pequeña
* Caja Media Express
* Caja Exprés Grande
* Marque la casilla de verificación **Paquete de asegurada**, para indicar que el paquete estará asegurado.
* Introduzca  **Cargo adicional de manipulación**. Es un cargo adicional para cobrar a sus clientes.
* Seleccione el  **Servicios de transportistas** que desea ofrecer a sus clientes.
* Compruebe para obtener tarifas para  ** Entrega de sábado habilitado**.
* Seleccione el  **Tipo de embalaje**, de la siguientemanera:
* Pack por dimensiones
* Empaquetar por un artículo por paquete
* Pack por volumen
* Marque la casilla de verificación **Pasar dimensiones**, para pasar las dimensiones del paquete al solicitar tarifas.
* Seleccione el  **Tipo de peso**  - libras o kilogramos.
* Seleccione el  **Tipo de dimensiones** - pulgadas o centímetros.
* Marque la casilla de verificación **Tracing** para registrar el seguimiento del sistema en el registro del sistema. Se registrará todo el XML de solicitud y respuesta (incluido AccessKey/Username, Password). No deje esto habilitado en un entorno de producción.

Haga clic en **Guardar**.



1. Click **Configure** beside the UPS (United Parcel Service) option in the list. 
    The *Configure – UPS (United Parcel Service)* window is displayed, as follows: ![Configure page](_static/ups/ups-configure.jpg)

1. Enter the following information obtained from the UPS provider:
    * Tick the **Use sandbox** checkbox to use testing environment.
    * Enter the **Account number** of the UPS provider.
    * Enter the **Access Key** obtained from the provider.
    * Enter your **Username** obtained from the provider.
    * Enter the **Password** obtained from the provider
    * Select your required **UPS Customer Classification**, as follows:
        * Rates Associated With Shipper Number
        * Daily Rates
        * Retail Rates
        * Regional Rates
        * General List Rates
        * Standard List Rates
    * Select the required **UPS Pickup Type**, as follows:
        * Daily Pickup
        * Customer Counter
        * One Time Pickup
        * On Call Air
        * Letter Center
        * Air Service Center
    * Select the required **UPS Packaging Type**, as follows:
        * Unknown
        * Letter
        * Customer Supplied Package
        * Tube
        * P A K
        * Express Box
        * 10 kg Box
        * 25 kg Box
        * Pallet
        * Small Express Box
        * Medium Express Box
        * Large Express Box
    * Tick the **Insure package** checkbox, to indicate the package will be insured.
    * Enter **Additional handling charge**. It is an additional fee to charge your customers.
    * Select the **Carrier Services** you want to offer to your customers.
    * Check to get rates for **Saturday Delivery enabled**.
    * Select the **Packing type**, as follows:
        * Pack by dimensions
        * Pack by one item per package
        * Pack by volume
    * Tick the **Pass dimensions** checkbox, to pass package dimensions when requesting for rates.
    * Select the **Weight type** - pounds or kilograms.
    * Select the **Dimensions type** - inches or centimeters.
    * Tick the **Tracing** checkbox, to record system tracing in the system log. The entire request and response XML will be logged (including AccessKey/Username, Password). Do not leave this enabled in a production environment.

    Click **Save**.