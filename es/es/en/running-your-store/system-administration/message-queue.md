---
title: Message queue
uid: en/running-your-store/system-administration/message-queue
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Cola de mensajes

Los correos electrónicos no se envían inmediatamente en nopCommerce. Están en cola. La cola de mensajes contiene todos los correos electrónicos que ya se han enviado o que aún no se han enviado.

Para cargar la cola de mensajes, en el menú **Sistema**, seleccione **Cola de mensajes**. Se muestra la ventana *Cola de mensajes*, de la siguiente manera:
!![Message queue item details](_static/message-queue/edit.jpg)

Introduzca uno o más de los siguientes criterios para buscar mensajes:
  * En el campo **Fecha de inicio**, seleccione la fecha de inicio.
  * En el campo **Fecha de finalización**, seleccione la fecha de finalización.
  * En el campo **From address**, introduzca la dirección de origen de un mensaje.
  * En el campo **Hacia la dirección**, ingrese la dirección de destino de un mensaje.
  * Marque la casilla de verificación **Cargar sólo correos electrónicos no enviados**, para cargar sólo los correos electrónicos que aún no han sido enviados.
  * En el campo **Máximo de intentos de envío**, introduzca el número máximo de intentos de envío de un mensaje.
  * En el campo **Ir directamente al correo electrónico#**, introduzca el número de correo electrónico y haga clic en **Ir** para mostrar el correo electrónico requerido.

Haga clic en **Buscar** para cargar la cola de mensajes que coincida con los criterios.

En esta página, puedes hacer clic en el botón **Borrar seleccionados** para eliminar los correos electrónicos seleccionados de la cuadrícula. Puedes hacer clic en **Borrar todo** para eliminar todos los correos electrónicos.

## Detalles del elemento de la cola de mensajes

Para ver los detalles de los elementos de la cola de mensajes, haga clic en el botón **Editar** junto al mensaje. Aparecerá la ventana *Editar elemento de la cola de mensajes*:

![Detalles de los artículos de la cola de mensajes](_static/message-queue/edit.jpg)

En esta ventana puede borrar el mensaje haciendo clic en el botón **Borrar**. O puede volver a poner en orden el mensaje usando el botón **Requeue**.

En esta página puedes editar los siguientes detalles del mensaje:

* **De** dirección de correo electrónico.
* **De nombre**.
* **Hasta** dirección de correo electrónico.
* **A nombre**.
* **Responder a la dirección de correo electrónico.
* **Responder a nombre**.
* **Cc** dirección de correo electrónico.
* **Bcc** dirección de correo electrónico.
* Mensaje de correo electrónico **Sujeto**.
* Mensaje de correo electrónico **Cuerpo**.
* Marque la casilla de verificación **Enviar inmediatamente** para enviar este mensaje inmediatamente.
* Introduce el número de **Intentos de envío**. Este es el número de veces para intentar enviar este mensaje.

Haga clic en **Save** o **Save y continúe editando** para guardar los detalles del mensaje. 