---
title: Installing on Microsoft Azure
uid: en/installation-and-upgrading/installing-nopcommerce/installing-on-microsoft-azure
author: git.AndreiMaz
contributors: git.skoshelev, git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# Instalación en Microsoft Azure

Hay tres formas de implementar nopCommerce en Microsoft Azure:

1. **FTP**. Utilice este método si ya tiene un paquete listo para implementar (sin código fuente). Puede publicar en un sistema de archivos local y luego cargar los archivos publicados a través de FTP.
  ¿Cómo obtener credenciales de FTP para Azure? Debe ir a [Azure.com](https://azure.microsoft.com/en-us/) → Mi cuenta → Portal de administración → Elija su sitio web → vaya a Panel de control → Vista rápida. Desde aquí puede encontrar las credenciales de FTP o puede * Restablecer sus credenciales de implementación * o * Descargar el perfil de publicación*.
  Para el nuevo portal azure, vaya a [portal.azure.com] (http://portal.azure.com/) → explore sitios web → navegue hasta su sitio web → Propiedades. Desde aquí puede encontrar las credenciales de FTP o puede *Restablecer sus credenciales de implementación* o *Descargar el perfil de publicación*.

1. **Visual Studio**: implementación web. También puede implementar directamente en azure desde Visual Studio. Descargue u obtenga las credenciales de implementación de azure usando la forma anterior y configure el perfil de implementación web en Visual Studio.

1. **Instalador de plataforma web**. nopCommerce está disponible en la galería de aplicaciones de sitios web de Azure. Así que vaya al portal de Azure, haga clic en "iniciar, nuevo sitio, desde la galería". Seleccione nopCommerce de la lista de aplicaciones disponibles. Después de ingresar la información de conexión de su base de datos y hacer clic en Aceptar, nopCommerce estará listo para iniciarse.

Una vez implementado el sitio, debe instalar nopCommerce. Lea más sobre esto [aquí](xref:es/installation-and-upgrade/installation-nopcommerce/index).

Azure admite varias instancias desde la versión 3.70. Es ideal para la escalabilidad de cualquier aplicación. Ahora no debe preocuparse si su sitio puede manejar una gran cantidad de visitantes. Entonces, ¿qué se ha hecho exactamente para admitir varias instancias en Azure y granjas web?

* **Soporte de cuenta de almacenamiento BLOB en Microsoft Azure**. Obtenga más información sobre las cuentas de almacenamiento en Azure [aquí] (https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/). *Cómo configurar:*
* Una vez que su almacenamiento BLOB esté configurado en Azure, abra su archivo `appsettings.json` (o` web.config` en versiones anteriores), busque el elemento **AzureBlobStorage** y especifique su cadena de conexión de almacenamiento BLOB, contenedor, punto final.
* **Soporte de gestión de sesiones y almacenamiento en caché distribuido**. [Redis] (http://redis.io/) ha sido elegido como servidor de almacenamiento en caché (ya disponible en Azure, Amazon y otras empresas de alojamiento en la nube). *Cómo configurar:*
* Primero, debes instalar y configurar Redis. Obtenga más información sobre cómo usar Redis en Azure [aquí] (https://azure.microsoft.com/en-us/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache/).*Una vez hecho esto, debe configurarlo en nopCommerce. Para habilitar el almacenamiento en caché en Redis, abra el archivo `appsettings.json` (o` web.config` en versiones anteriores). Busque elementos de configuración **RedisEnabled** y **UseRedisForCaching** (**RedisCaching** en versiones anteriores). Configúrelos en *true* y luego especifique **RedisConnectionString** apuntando a su servidor Redis (configurado en el primer paso).
* Para las versiones 3.90 (y anteriores), también debe habilitar Redis como nuestra administración de sesión distribuida. Abra el archivo `web.config`. Busque y elimine el comentario del elemento **sessionState**. Especifique sus atributos (*host*, *accessKey*, etc.) apuntando a su servidor Redis.
* Configuración recomendada del archivo `appsettings.json` para mejorar la estabilidad:
* **UsePluginsShadowCopy**: configúrelo en *false* para evitar el problema con el reciclaje del grupo de IIS y el escalado horizontal.
* Asegúrese de que las tareas de programación de nopCommerce se ejecuten en un nodo de la granja a la vez. Para configurar esto (para las versiones 3.90 y anteriores):
  * Para habilitar esta funcionalidad, abra el archivo `web.config`, busque el elemento **WebFarms** y establezca su atributo **MultipleInstancesEnabled** en *true*. Si utiliza sitios web de Microsoft Azure (no servicios en la nube), establezca también el atributo **RunOnAzureWebsites** en *true*.