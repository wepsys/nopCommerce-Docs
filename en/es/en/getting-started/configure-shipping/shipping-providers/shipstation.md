---
title: ShipStation
uid: en/getting-started/configure-shipping/shipping-providers/shipstation
author: git.mariannk, git.skoshelev
---

* ShipStation

Para utilizar el plugin de integración **ShipStation**,  siga estos pasos:

1. Regístrese o inicie sesión en elsitio [ShipStation](https://www.shipstation.com/?ref=partner-nopcommerce&utm_campaign=partner-referrals&utm_source=nopcommerce&utm_medium=partner-referral).
1. En el área de administración de nopCommerce vaya a  **Configuración > Envío > Proveedores de envío**.
![Métodos de tarifa de envío](_static/shipstation/shipping-rate-methods.jpg)
* Habilite este método, como se indica a continuación:
* En la fila ShipStation, haga clic en el botón  Editar.
* En la columna **Está activo**,  marque la casilla de verificación.
* Haga clic en el botón **Actualizar**.  La opción false se convierte en  **true**.
* Haga clic en el botón Configurar junto a la opción ShipStation de la lista. Se muestra la ventana *Configurar - ShipStation*,  como se indica a continuación: ![ Configurar página](_static/shipstation/shipstation-configure.jpg)
1. Introduzca la siguiente información obtenida del proveedor ShipStation:
* La  clave DE API y el secreto de API :estos datos se utilizan para obtener una lista de losoperadores disponibles. Puede obtenerlos en la página *Configuración - Configuración de API*  del sitio de ShipStation.
> [!Nota]
> Si no tiene previsto utilizar la determinación automática del coste de envío, no es necesario introducir estos datos.
> Pero en este caso, el plugin dejará de funcionar como proveedor de métodos de envío y tendrá que asegurarse de que hay otro plugin activo del mismo tipo.

* Crear un  **Nombre de usuario**  y  **Contraseña**,introdúzcalos en el formulario de configuración (el formulario ShipStation y el formulario nopCommerce). Estos datos son necesarios para la transferencia segura de datos entre el servidor y el servidor ShipStation. Mantenlos siempre en secreto.

> [!Importante]
> No utilice las credenciales de usuario de ShipStation o nopCommerce para estos campos.

* Marque la casilla de verificación **Pasar dimensiones**  si es necesario enviar dimensiones al servidor ShipStation. Cuando se activa este parámetro, aparece el parámetro adicional **Tipo de embalaje**.  Este parámetro es responsable del tipo de datos enviados. ![Tipo de embalaje](_static/shipstation/packing-type.jpg)

