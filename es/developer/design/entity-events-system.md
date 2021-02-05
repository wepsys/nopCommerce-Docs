---
title: Entity events system
uid: es/developer/design/entity-events-system
author: git.nopsg
contributors: git.nopsg, git.DmitriyKulagin
---

# Sistema de eventos de la entidad

## Visión general

nopCommerce implementa una arquitectura impulsada por eventos que permite a los desarrolladores suscribirse o consumir eventos transmitidos por los editores de eventos o la fuente de eventos cuando se realiza alguna acción/evento y también nos permite realizar cierta lógica comercial cuando se desencadena algún evento específico. En nopCommerce, podemos suscribirnos o escuchar varios eventos publicados por el evento del sistema nopCommerce o incluso podemos escribir una lógica que emite/publica un evento que luego se puede escuchar o suscribir. Por ejemplo, supongamos que queremos sincronizar los detalles del cliente con algún otro sistema externo, por lo que, en ese caso, podemos activar un evento cuando un nuevo cliente se registre en nuestra tienda o un cliente cambie su perfil. Podemos escuchar ese evento y realizar la lógica comercial que luego puede extraer ese cliente recién creado y enviarlo al servicio externo para sincronizarlo. Y la mejor parte es que podemos hacer todo esto sin cambiar el código fuente de nopCommerce.

Los desarrolladores pueden publicar un evento o consumir un evento:

- Para publicar un evento, un desarrollador deberá obtener una instancia de **IEventPublisher** y llamar al método **Publish** con los datos del evento apropiados.

- Para escuchar un evento, el desarrollador querrá crear una nueva implementación de la interfaz genérica **IConsumer**. Una vez que se ha creado una nueva implementación de consumidor, nopCommerce usa la reflexión para encontrar y registrar la implementación para el manejo de eventos.

Hay tres métodos de extensión del editor de eventos que se utilizan para eventos de modificación de datos denominados `EntityInserted`,`EntityUpdated` y `EntityDeleted` con **BaseEntity** heredan de la interfaz **IEventPublisher** que es responsable de difundir la inserción, actualización y eliminar eventos de entidad respectivamente.

## EntityInserted

Este método de extensión toma la entidad modelo de tipo "BaseEntity" como parámetro. Este método de extensión se utiliza para publicar/difundir el evento de entidad insertada de tipo `BaseEntity` cuando se insertan nuevos datos. Este método de extensión luego invoca el constructor parametrizado de la clase genérica EntityInsertedEvent y expone la entidad insertada por su propiedad Entity. Que luego puede ser suscrito/manejado por el desarrollador implementando la interfaz IConsumer de tipo EntityInsertedEvent de tipo Entity que insertamos recientemente, por ejemplo: `IConsumer <EntyInsertedEvent <BaseEntity>>`. Aquí, `BaseEntity` puede ser cualquier clase de modelo que herede de la clase `BaseEntity`.

### Implementación del editor para el evento EntityInserted

```cs
public class MyFirstPublisherClass
{
    IEventPublisher _eventPublisher;
    public MyFirstPublisherClass(IEventPublisher eventPublisher)
    {
        this._eventPublisher = eventPublisher;
    }

    public void MyFirstProductInsertMethod(Product product)
    {
        //La lógica para insertar va aquí
        _eventPublisher.EntityInserted<Product>(product);
    }
}
```

En el ejemplo anterior, estamos inyectando la interfaz `IEventPublisher` para obtener la instancia de la clase EventPublisher usando el mecanismo de inyección de dependencia del constructor. Aquí en `MyFirstProductInsertMethod` después de completar la lógica para insertar el producto, estamos invocando el método `EntityInserted` con un tipo genérico de `Product` (que debe heredarse de la clase BaseEntity) con el objeto de producto recién creado como parámetro. Ahora, al invocar este método de extensión, transmitirá el evento insertado por la entidad para el tipo de producto y ahora quien esté suscrito/escuchando este evento recibirá este objeto de producto como un parámetro de evento. Ahora veamos cómo consumir este evento.

### Implementación del consumidor para el evento EntityInserted

```cs
public class MyFirstConsumerClass : IConsumer<EntityInsertedEvent<Product>>
{
    public void HandleEvent(EntityInsertedEvent<Product> insertEvent)
    {
        //puede acceder a la entidad usando insertEvent.Entity
        var insertedEntity = insertEvent.Entity;

        //Aquí va la lógica empresarial que desea realizar ...

    }
}
```

Aquí estamos creando una clase que es inherente a `IConsumer <EntityInsertedEvent <Product>>`. La interfaz `IConsumer` tiene solo un método que debe implementarse, es decir, el método `HandleEvent`. Ahora, siempre que se active el evento EntityInserted de tipo Product, este método `HandleEvent` se invocará con `EntityInsertedEvent` de tipo objeto de entidad de producto. Y aquí, dentro de esta clase, podemos realizar nuestra lógica de negocios para el procesamiento posterior de esos datos.

## EntityUpdated

Este método de extensión de la interfaz `IEventPublisher` también se implementa de la misma manera que EntityInserted. Este método de extensión también toma la entidad modelo de tipo `BaseEntity` como argumento/parámetro. Este método de extensión se utiliza para publicar/difundir el evento actualizado de la entidad del tipo `BaseEntity` cuando se actualiza una entidad existente. Este método de extensión invoca el constructor parametrizado de la clase genérica `EntityUpdatedEvent` y expone la entidad actualizada por su propiedad Entity. Que luego puede ser suscrito/manejado por el desarrollador implementando la interfaz IConsumer del tipo `EntityUpdatedEvent` del tipo `Entity` que insertamos recientemente, por ejemplo: `IConsumer <EntyUpdatedEvent <BaseEntity>>`.

### Implementación del editor para el evento EntityUpdated

```cs
public class MyFirstPublisherClass
{
    IEventPublisher _eventPublisher;
    public MyFirstPublisherClass(IEventPublisher eventPublisher)
    {
        this._eventPublisher = eventPublisher;
    }

    public void MyFirstProductUpdateMethod(Product product)
    {
        //La lógica para insertar va aquí
        _eventPublisher.EntityUpdated<Product>(product);
    }
}
```

The implementation of this class is moreover the same as the example in the `EntityInserted`. Here in `MyFirstProductInsertMethod` after completing the logic to update product we are invoking `EntityUpdated` method with a generic type of with recently updated product object as a parameter. Now upon invoking this extension method, it will broadcast entity updated event for product type and now whoever is subscribing/listening for this event will receive this product object as an event parameter. Now let's see how to consume this event.

### Consumer Implementation for EntityUpdated Event

```cs
public class MyFirstConsumerClass : IConsumer<EntityUpdatedEvent<Product>>
{
    public void HandleEvent(EntityUpdatedEvent<Product> updateEvent)
    {
        //puede acceder a la entidad usando updateEvent.Entity
        var updatedEntity = updateEvent.Entity;

        //Aquí va la lógica empresarial que desea realizar ...

    }
}
```

Nuevamente, esto también es igual que la clase de consumidor para el evento insertado por entidad. Aquí estamos creando una clase que hereda de `IConsumer <EntityUpdatedEvent <Product>>`. Ahora, siempre que se active el evento `EntityUpdated` de tipo`Product`, se invocará el método `HandleEvent` de esta clase con el parámetro de objeto de entidad de producto de tipo `EntityUpdatedEvent`. Y aquí, dentro de esta clase, podemos realizar nuestra lógica de negocios para el procesamiento posterior de esos datos.

## EntityDeleted

La lógica para implementar este método de extensión también es la misma que la del método de extensión `EntityInserted` y `EntityUpdated` de `IEventPublisher`. Este método de extensión también toma la entidad modelo de tipo `BaseEntity` como argumento. Este método de extensión se utiliza para publicar/difundir el evento de entidad eliminada de "BaseEntity" cuando se elimina una entidad existente. Este método de extensión invoca al constructor de la clase genérica `EntityDeletedEvent` y expone la entidad eliminada por su propiedad Entity. Que luego puede ser suscrito/manejado por el desarrollador implementando `IConsumer <EntityDeletedEvent <BaseEntity>>`.

### Publisher Implementation for EntityDeleted Event

```cs
public class MyFirstPublisherClass
{
    IEventPublisher _eventPublisher;
    public ExamplePublisherClass(IEventPublisher eventPublisher)
    {
        this._eventPublisher = eventPublisher;
    }

    public void MyFirstProductDeleteMethod(Product product)
    {
        //La lógica para insertar va aquí
        _eventPublisher.EntityDeleted<Product>(product);
    }
}
```

La implementación de esta clase también es la misma que en el ejemplo anterior. Aquí, en `MyFirstProductDeleteMethod` después de completar la lógica para eliminar el producto, estamos invocando el método `EntityDeleted` con el objeto de producto que borramos recientemente como parámetro. Ahora, al invocar este método de extensión, transmitirá el evento de entidad eliminada para el tipo de producto y ahora quien se suscriba/escuche este evento recibirá este objeto de producto como parámetro de evento. Ahora veamos cómo consumir este evento.

### Implementación del consumidor para el evento EntityDeleted

```cs
public class MyFirstConsumerClass : IConsumer<EntityDeletedEvent<Product>>
{
    public void HandleEvent(EntityDeletedEvent<Product> deleteEvent)
    {
        //puede acceder a la entidad usando deleteEvent.Entity
        var updatedEntity = deleteEvent.Entity;

        //Aquí va la lógica empresarial que desea realizar ...

    }
}
```

Nuevamente, esto también es igual que la clase de consumidor para el evento insertado por entidad o el evento actualizado por entidad. Aquí estamos creando una clase que hereda de `IConsumer <EntityDeletedEvent <Product>>`.

Ahora, siempre que se active el evento `EntityDeleted` de tipo Product, se invocará el método `HandleEvent` de esta clase con el parámetro del objeto de entidad de producto de tipo `EntityDeletedEvent`. Y aquí, dentro de esta clase, podemos realizar nuestra lógica de negocios para el procesamiento posterior de esos datos.
