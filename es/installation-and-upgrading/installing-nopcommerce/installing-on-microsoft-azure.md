---
title: Installing on Microsoft Azure
uid: es/installation-and-upgrading/installing-nopcommerce/installing-on-microsoft-azure
author: git.AndreiMaz
contributors: git.skoshelev, git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# Instalación en Microsoft Azure

Hay tres maneras de implementar nopCommerce en Microsoft Azure:

1. **FTP**. Utilice este método si ya tiene un paquete listo para implementar (sin código fuente). Puede publicar en un sistema de archivos local y, a continuación, cargar los archivos publicados a través de FTP. 
¿Cómo obtener credenciales FTP para Azure? Usted debe ir [Azure.com](https://azure.microsoft.com/en-us/) → Mi cuenta → Portal de administración → Elija su sitio web → ir a Panel de control -mirada rápida. Desde aquí puede encontrar las credenciales FTP o puede  *Restablecer sus credenciales de implementación*  o  *Descargar el perfil de publicación*.
Para el nuevo portal azul vaya [portal.azure.com](http://portal.azure.com/) → navegar por los sitios web → navegar a su sitio web→ Propiedades. Desde aquí puede encontrar las credenciales FTP o puede  *Restablecer sus credenciales de implementación*  o  *Descargar el perfil de publicación*.

1. **Visual Studio**  - implementación web. También puede implementar directamente en azure desde visual studio. Descargue u obtenga las credenciales de implementación de azure utilizando la forma anterior y configurar el perfil de implementación web en Visual Studio.

1. **Instalador de plataforma web**. nopCommerce está disponible en la galería de aplicaciones de Azure Web Sites. Así que vaya a Azure Portal, haga clic en "inicio, nuevo sitio, desde la galería". Selecciona nopCommerce en la lista de aplicaciones disponibles. Después de introducir la información de conexión de la base de datos y hacer clic en Aceptar, nopCommerce estará listo para iniciarse.

Una vez que el sitio está implementado tienes que instalar nopCommerce. Por favor, lea más sobre él [aquí](xref:en/installation-and-upgrading/installing-nopcommerce/index).

Azure es compatible con varias instancias desde la versión 3.70. Es ideal para cualquier escalabilidad de aplicaciones. Ahora no debe preocuparse si su sitio puede manejar un gran número de visitantes. Entonces, ¿qué se ha hecho exactamente para admitir varias instancias en Azure y granjas de servidores web?

* **Soporte de cuenta de almacenamiento BLOB en Microsoft Azure**. Obtenga más información sobre las cuentas de almacenamiento en Azure [aquí](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/). *Cómo configurar:*
  * Una vez configurado el almacenamiento BLOB en Azure, abra el archivo `appsettings.json`  (o `web.config` en versiones anteriores), busque el elemento **AzureBlobStorage** y especifique la cadena de conexión de almacenamiento BLOB, el contenedor y el punto de conexión.
* **Almacenamiento en caché distribuido y soporte de administración de sesiones**. [Redis](http://redis.io/) se ha elegido como un servidor de almacenamiento en caché(ya disponible en Azure, Amazon, otras empresas de hospedaje en la nube). *Cómo configurar:*
  * En primer lugar, usted tiene que instalar y configurar Redis. Encontrará más información sobre cómo usar Redis en Azure [aquí](https://azure.microsoft.com/en-us/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache/).
* Una vez hecho esto tienes que configurarlo en nopCommerce. Para habilitar el almacenamiento en caché en Redis, abra el archivo `appsettings.json`  (o `web.config` en versiones anteriores). Busque los elementos de configuración De **RedisEnabled** y **UseRedisForCaching**(**RedisCaching**en   versiones anteriores). Establézcalos en *true* y, a continuación, especifique  **RedisConnectionString**  apuntando el servidor de Redis (configurado en el primer paso).
  * Para las versiones 3.90 (y a continuación) también tiene que habilitar Redis como nuestra gestión de sesiones distribuidas. Abra el archivo `web.config`. Busque y descomprima el elemento **sessionState**. Especifique sus atributos (*host*, *accessKey*, etc.) que apuntan a su servidor de Redis.
* Ajustes recomendados del archivo 'appsettings.json' para mejorar la estabilidad:
  * **UsePluginsShadowCopy** → establézcalo en  *false*  para evitar el problema con el reciclaje del grupo de IIS y el escalado horizontal.
* Asegúrese de que las tareas de programación de nopCommerce se ejecutan en un nodo de granja de servidores a la vez. Para configurar esto (para las versiones 3.90 y siguientes):
* Para habilitar esta funcionalidad, abra el archivo `web.config`,  busque el elemento WebFarms y establezca su  atributo  MultipleInstancesEnabled en *true*. Si usa sitios web de Microsoft Azure (no servicios en la nube), establezca también el  atributo RunOnAzureWebsites en *true*.