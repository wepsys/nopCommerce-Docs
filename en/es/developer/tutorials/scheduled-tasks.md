---
title: Scheduled Tasks
uid: en/developer/tutorials/scheduled-tasks
author: git.AndreiMaz
contributors: git.sinaislam, git.DmitriyKulagin, git., git.exileDev
---

# Tareas programadas

Con las tareas programadas, puede programar una tarea para que se ejecute en determinados períodos. Por ejemplo, nopCommerce envía correos electrónicos en cola periódicamente. Los pasos básicos para crear una nueva tarea son:

1. Defina una clase que implemente la interfaz **IScheduleTask**. Tiene un solo método que no toma argumentos; **Ejecutar**. Como adivinó, este método se invoca cuando se debe ejecutar la tarea.

1. Para programar una tarea, el desarrollador debe insertar un nuevo registro **ScheduleTask** en la tabla de base de datos correspondiente. Puede utilizar **IScheduleTaskService** para insertar dicho registro.

> [!IMPORTANT]
>
> Cuando inserte el nuevo registro en la tabla de base de datos **ScheduleTask** para la nueva **ScheduleTask**, es importante mantener el formato de columna **Tipo**  **Espacio de nombres.TaskClassName, AssemblyName**.

## Solución de problemas

- Asegúrese de que su tienda tenga una URL válida.
- Reinicie la aplicación después de agregar una nueva tarea programada.
