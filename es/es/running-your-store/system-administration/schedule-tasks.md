---
title: Schedule tasks
uid: en/running-your-store/system-administration/schedule-tasks
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Programar tareas

La ventana *Programar tareas* permite al propietario de la tienda programar una tarea para que se ejecute durante ciertos períodos en segundo plano y ver información útil sobre la tarea y si se completó correctamente. Por ejemplo, nopCommerce envía correos electrónicos en cola periódicamente. Las tareas se ejecutan en un hilo independiente procedente del grupo de hilos ASP.NET.

Para ver las tareas programadas, en el menú **Sistema**, seleccione **Programar tareas**. Se muestra la ventana *Programar tareas*, de la siguiente manera:
![Programar tareas](_static/schedule-tasks/schedule-tasks.png)

Para editar una tarea programada, haga clic en el botón **Editar** junto a la tarea. La ventana se expande de la siguiente manera:
! [Programar tareas - Editar] (_static/schedule-tasks/schedule-tasks-edit.png)

Puede editar la tarea programada de la siguiente manera:
* Edite el **Nombre**.
* Edite el número de **Segundos (período de ejecución)**. El período de la tarea no debe exceder los 24 días.
* Marque la casilla de verificación **Habilitado** para habilitar la tarea.
* Marque la casilla de verificación **Detener en caso de error** para detener la tarea cuando se produzca un error.

Haga clic en **Actualizar** para guardar sus cambios.

> [!NOTA]
>
> No olvide reiniciar la aplicación una vez que se haya modificado una tarea.

Si es necesario, puede hacer clic en **Ejecutar ahora**, para ejecutar una tarea programada bajo demanda.