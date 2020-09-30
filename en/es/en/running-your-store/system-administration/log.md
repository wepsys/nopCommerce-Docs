---
title: Log
uid: en/running-your-store/system-administration/log
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Log

El informe del log del sistema muestra una lista de todos los errores, advertencias y mensajes de información que se crearon en el sistema. Para ver el log vaya a **System → Log**. La ventana *Log* se muestra como sigue:

![Log](_static/log/log.png)

Un elemento de registro incluye el tipo de registro, la descripción del error y la fecha. Puede hacer clic en el botón **Borrar seleccionado** para eliminar los elementos de registro seleccionados o hacer clic en el botón **Borrar registro** para borrar todo el registro.

Para buscar el registro del sistema, introduzca una o más de las siguientes informaciones:
  * En el campo **Creado desde**, seleccione la fecha de inicio de la búsqueda.
  * En el campo **Creado hasta**, seleccione la fecha final de la búsqueda.
  * En el campo **Mensaje**, seleccione el mensaje o parte del mensaje por el que desea realizar la búsqueda.
  * En la lista desplegable **Nivel de registro**, seleccione el tipo de información de registro a mostrar, como sigue:
    * *Todos*
    * * Debug *
    * * Información *
    * * Advertencia *
    * * Error *
    * * Fatal *

Haz clic en **Búsqueda**. La ventana del sistema de registro se mostrará en función de los criterios de búsqueda.

## Ver detalles del registro del sistema

Al hacer clic en **Ver** se muestran detalles adicionales del error que ocurrió, de la siguiente manera:

![Log entry - Details](_static/log/log-details.jpg)


Puede pulsar **Borrar** para eliminar un registro del sistema si es necesario.