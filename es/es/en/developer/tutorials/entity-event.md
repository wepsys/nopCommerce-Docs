---
title: Entity events and how they work
uid: en/developer/tutorials/entity-event
author: git.sinaislam
contributors: git.DmitriyKulagin
---

# Eventos de la entidad y cómo funcionan

Los métodos de extensión **EntityInserted**, **EntityUpdated** y **EntityDeleted** (https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/extension-methods) con **BaseEntity** [constraint](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters) de la interfaz **IEventPublisher** se encargan de difundir la entidad insertada, actualizada y eliminada respectivamente.

1. El método de extensión **EntityInserted** se invoca para publicar una entidad insertada. Invoca el constructor parametrizado de la **EntityInsertedEvent** [clase genérica](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y expone la entidad insertada por su propiedad **Entity**. La **EntidadInsertadaEvento** tiene la misma restricción que la **EntidadInsertada**. El desarrollador puede obtener la nueva entidad insertada mediante la implementación de la interfaz **Consumidor** y puede hacer otros trabajos necesarios.

1. El método de extensión **EntityUpdated** de la interfaz **IEventPublisher** se implementa de la misma manera que **EntityInserted**. Este método de extensión se llama cuando se actualiza una entidad existente. Invoca al constructor parametrizado de **EntityUpdatedEvent** [clase genérica](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y expone la entidad actualizada por su propiedad **Entity**. **EntityUpdatedEvent** tiene la misma restricción de **EntityUpdated**. Al implementar la interfaz **Consumidor** el desarrollador puede obtener la entidad actualizada.

1. El método de extensión **EntityDeleted** de la interfaz **IEventPublisher** se implementa de la misma manera que **EntityInserted** y **EntityUpdated**. Este método de extensión se llama cuando se elimina una entidad existente. Invoca al constructor parametrizado de **EntityDeletedEvent** [clase genérica](https://docs.microsoft.com/dotnet/csharp/programming-guide/generics/generic-classes) y publica la entidad eliminada por su propiedad **Entity**. **EntityDeletedEvent** tiene la misma restricción de **EntityDeleted**.  Al implementar la interfaz **Consumidor** el desarrollador puede obtener la entidad eliminada.
