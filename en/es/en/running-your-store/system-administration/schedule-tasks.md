---
title: Schedule tasks
uid: en/running-your-store/system-administration/schedule-tasks
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Programe las tareas

La ventana *Programar tareas* permite al propietario de la tienda programar una tarea para que se ejecute durante determinados períodos en segundo plano y ver información útil sobre la tarea y si se completó con éxito. Por ejemplo, nopCommerce envía periódicamente correos electrónicos en cola. Las tareas se ejecutan en un hilo independiente que proviene del grupo de hilos de ASP.NET.

Para ver las tareas programadas, en el menú **Sistema**, seleccione **Programar tareas**. Se muestra la ventana *Programar tareas*, de la siguiente manera:
![Schedule tasks](_static/schedule-tasks/schedule-tasks.png)

Para editar una tarea programada, haga clic en el botón **Editar** al lado de la tarea. La ventana se expande, como sigue:
![Schedule tasks - Edit](_static/schedule-tasks/schedule-tasks-edit.png)

Puedes editar la tarea programada de la siguiente manera:
* Editar el **Nombre**.
* Editar el número de **Segundos (período de ejecución)**. El período de la tarea no debe exceder los 24 días.
* Marque la casilla de verificación **Habilitado** para habilitar la tarea.
* Marque la casilla de verificación **Detener en error** para detener la tarea cuando se produzca un error.

Haga clic en **Actualizar** para guardar los cambios.

> [!NOTE]
>
> No olvide reiniciar la aplicación una vez que una tarea haya sido modificada.

Si es necesario, puede hacer clic en **Ejecutar ahora**, para ejecutar una tarea programada a petición.