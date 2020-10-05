---
title: Exposing and Handling Events
uid: en/developer/tutorials/events
author: git.AndreiMaz
contributors: git.exileDev
---

# Exposición y manejo de eventos

Los eventos son notificaciones que se transmiten a las partes interesadas. Los eventos se activan en los cambios de datos como inserciones, actualizaciones y eliminaciones. nopCommerce permite a los desarrolladores "escuchar" eventos en los que podrían estar interesados. Hay dos formas en que un desarrollador trabajará con eventos. Un desarrollador querrá publicar eventos para que los oyentes los consuman o suscribirse a eventos que otros desarrolladores hayan publicado mediante programación.

1. Para publicar un evento, un desarrollador deberá obtener una instancia de **IEventPublisher** y llamar al método **Publish** con los datos del evento apropiados.
1. Para escuchar un evento, el desarrollador querrá crear una nueva implementación de la interfaz genérica **IConsumer**. Una vez que se ha creado una nueva implementación de consumidor, nopCommerce usa la reflexión para encontrar y registrar la implementación para el manejo de eventos.
