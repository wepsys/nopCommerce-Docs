---
title: Entity events and how they work
uid: es/developer/tutorials/entity-event
author: git.sinaislam
contributors: git.DmitriyKulagin
---

# Eventos de entidad y cómo funcionan

Los [métodos_de_extensión]**EntityInserted**, **EntityUpdated** y **EntityDeleted** (https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/extension-methods) con **BaseEntity** [restricción](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters) de la interfaz **IEventPublisher** son responsables de transmitir la entidad insertada, actualizada y eliminada respectivamente.

1. Se invoca el método de extensión **EntityInserted** para publicar una entidad insertada. Invoca el constructor parametrizado de **EntityInsertedEvent** [clase genérica](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y expone la entidad insertada por su **Propiedad** de la entidad. **EntityInsertedEvent** tiene la misma restricción que **EntityInserted**. El desarrollador puede obtener la nueva entidad insertada implementando la interfaz **IConsumer** y puede hacer otros trabajos necesarios.

1. El método de extensión **EntityUpdated** de la interfaz **IEventPublisher** se implementa de la misma manera que **EntityInserted**. Este método de extensión se llama cuando se actualiza una entidad existente. Invoca el constructor parametrizado de **EntityUpdatedEvent** [clasegenérica] (https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y expone la entidad actualizada por su **Entidad** propiedad. **EntityUpdatedEvent** tiene la misma restricción de **EntityUpdated**. Al implementar la interfaz **IConsumer**, el desarrollador puede obtener la entidad actualizada.

1. El método de extensión **EntityDeleted** de la interfaz **IEventPublisher** se implementa de la misma manera que **EntityInserted** y **EntityUpdated**. Este método de extensión se llama cuando se elimina una entidad existente. Invoca el constructor parametrizado de **EntityDeletedEvent** [clase genérica](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y publica la entidad eliminada por su **Entidad** propiedad.**EntityDeletedEvent** tiene la misma restricción de **EntityDeleted**. Al implementar la interfaz **IConsumer**, el desarrollador puede obtener la entidad eliminada.