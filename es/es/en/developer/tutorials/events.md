---
title: Exposing and Handling Events
uid: en/developer/tutorials/events
author: git.AndreiMaz
contributors: git.exileDev
---

# Exponer y manejar eventos

Los eventos son notificaciones que se transmiten a las partes interesadas. Los eventos se activan con los cambios de datos como inserciones, actualizaciones y eliminaciones. nopCommerce permite a los desarrolladores "escuchar" los eventos que podrían interesarles. Hay dos formas en que un desarrollador trabajará con los eventos. Un desarrollador querrá publicar eventos para que los oyentes los consuman, o suscribirse a eventos que otros desarrolladores habrán publicado programáticamente.

1. Para publicar un evento un desarrollador necesitará obtener una instancia de **IEventPublisher** y llamar al método **Publish** con los datos del evento apropiado.
1. Para escuchar un evento el desarrollador querrá crear una nueva implementación de la interfaz genérica de **Consumidor**. Una vez que una nueva implementación de consumo ha sido creada nopCommerce utiliza la reflexión para encontrar y registrar la implementación para el manejo de eventos.
