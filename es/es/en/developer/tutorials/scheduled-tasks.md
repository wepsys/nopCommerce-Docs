---
title: Scheduled Tasks
uid: en/developer/tutorials/scheduled-tasks
author: git.AndreiMaz
contributors: git.sinaislam, git.DmitriyKulagin, git., git.exileDev
---

# Tareas programadas

Con las tareas programadas, se puede programar una tarea para que se ejecute en determinados períodos. Por ejemplo, nopCommerce envía periódicamente correos electrónicos en cola. Los pasos básicos para crear una nueva tarea son:

1. Definir una clase que implemente la interfaz **IScheduleTask**. Sólo tiene un método que no toma argumentos; **Ejecutar**. Como has adivinado, este método es invocado cuando la tarea debe ser ejecutada.

1. Para programar una tarea el desarrollador debe insertar un nuevo registro **ScheduleTask** en la tabla de la base de datos apropiada. Puede utilizar **IScheduleTaskService** para insertar dicho registro.

> [!IMPORTANT]
> 
> Cuando se inserte el nuevo registro en la tabla de la base de datos de **ScheduleTask** para el nuevo **ScheduleTask**, es importante mantener el formato de columna **Namespace.TaskClassName, AssemblyName**.

## Solución de problemas

- Asegúrate de que tu tienda tenga una URL válida.
- Reinicie la aplicación después de agregar una nueva tarea programada.
