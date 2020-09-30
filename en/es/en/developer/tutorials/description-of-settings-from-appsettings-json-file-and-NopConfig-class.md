---
title: Description settings from appsettings.json file and NopConfig and HostingConfig class
uid: en/developer/tutorials/description-of-settings-from-appsettings-json-file-and-NopConfig-class
author: git.nopsg
contributors: git.nopsg, git.DmitriyKulagin
---

# Descripción de la configuración del archivo appsettings.json y la clase NopConfig y HostingConfig

## Visión general

Este artículo contiene una descripción del archivo `appsettings.json` y la `clase NopConfig`. En este artículo explicaremos cuáles son las diferentes configuraciones disponibles en estos archivos, qué hace cada configuración y cuándo usar esta configuración para cambiar la funcionalidad / comportamiento del proyecto nopCommerce.

## descripción general del archivo appsettings.json

Si ha trabajado anteriormente en el proyecto `ASP.NET core` o está familiarizado con el`ASP.NET core`, entonces es posible que haya usado el archivo `appsettings.json` y tenga cierta comprensión de qué es este archivo y para qué se usa. para.

El archivo `appsettings.json` se usa generalmente para almacenar los ajustes de configuración de la aplicación, como cadenas de conexión de la base de datos, cualquier variable global del alcance de la aplicación y mucha otra información. En realidad, en `ASP.NET Core`, la configuración de la aplicación se puede almacenar en diferentes fuentes de configuración, como el archivo`appsettings.json`, el archivo `appsettings. {EnvironmentName} .json` (donde {Environment} es el alojamiento actual de la aplicación entornos como desarrollo, puesta en escena o producción), `secretos de usuario` (donde solíamos almacenar información confidencial), etc.

equilibrador de carga y si está habilitando la configuración **`UseHttpClusterHttps` **anterior. Esta configuración se usa para agregar** `X-Fordered-Proto`** en la configuración`HTTP` ##disponible en el archivo appsettings.json

g.### Hosting

Hosting contains settings used to configure the hosting behavior. It is a json object and contains some properties settings which can be tweak to change the behavior for hostin
### Alojamiento

El alojamiento contiene la configuración que se utiliza para configurar el comportamiento del alojamiento. Es un objeto json y contiene algunas configuraciones de propiedades que se pueden modificar para cambiar el comportamiento del alojamiento.

#### UseHttpXForderedProto

Esta configuración espera un valor booleano. El valor predeterminado es "**falso**". Es posible que desee establecer el valor en "**verdadero**" si su alojamiento utiliza un encabezado. **`X-Fordered-Proto`** es un encabezado HTTP y es parte del estándar HTTP. Se establece en cada solicitud HTTP por un proxy o equilibrador de carga y puede ser utilizado por una aplicación de servidor para determinar qué protocolo utilizó el cliente para conectarse.

#### ForderedHttpHeader

Esta configuración espera un valor de cadena. Puede utilizar esta configuración si su alojamiento no utiliza el encabezado "" X-FORWARDED-FOR "` para determinar la dirección IP. En algunos casos, el servidor utiliza otro encabezado HTTP. Puede especificar un encabezado HTTP personalizado aquí. Por ejemplo, CF-Connecting-IP, X-FORWARDED-PROTO, etc.

### Nop

Nop contiene ajustes que se utilizan para configurar el comportamiento de nopCommerce. Es un objeto json y contiene algunas configuraciones de propiedades que se pueden modificar para cambiar el comportamiento de nopCommerce.

#### DisplayFullErrorStack

Esta configuración espera un valor booleano. El valor predeterminado es **`falso`**. Puede establecer el valor en **`verdadero`** si desea ver el error completo en el entorno de producción. Que no es lo que solemos sugerir. Pero si tiene una buena razón para mostrar un error completo durante el entorno de producción, puede hacerlo desde esta configuración. Para el entorno de desarrollo, esta configuración se ignora y cualquiera que sea el valor que establezca para esta configuración, se mostrará el error completo. Podemos decir que esta configuración siempre está habilitada para el entorno de desarrollo.

#### Azure Blob Storage

Podemos usar ``Azure Blob Storage`` para almacenar datos de blobs. nopCommerce ya tiene una función integrada para eso, solo necesitamos configurar la siguiente información correctamente para usar / habilitar esta función. Los valores de esta configuración se pueden obtener para Azure mientras crea la cuenta de almacenamiento.

* **AzureBlobStorageConnectionString:** Esta configuración espera un valor de cadena. Aquí debe agregar su cadena de conexión `AzureBlobStorage`
* **AzureBlobStorageContainerName:** El valor de esta configuración también es de tipo cadena. En esta configuración, establecemos el nombre del contenedor para el almacenamiento de Azure BLOB.
* **AzureBlobStorageEndPoint:** Esta configuración también espera un valor de cadena. Aquí tenemos que establecer el punto final para el almacenamiento de Azure BLOB.
* **AzureBlobStorageAppendContainerName:** Esta configuración espera un valor booleano. Establezca el valor en **`true`** o **`false`** en función de si el nombre del contenedor se anexa al `AzureBlobStorageEndPoint` al construir la URL.

#### Redis

nopCommerce admite *Redis* listo para usar. Para habilitar el `Redis` en nuestra aplicación, debemos establecer el valor apropiado para las siguientes configuraciones. Para obtener más información sobre [Redis](https://azure.microsoft.com/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache).

* **RedisEnabled:** Esta configuración espera un valor booleano. Establezca el valor en **"verdadero"** si desea habilitar `Redis`.
* **RedisDatabaseId:** ID de la base de datos de Redis. Si necesita utilizar una base de datos de Redis específica, simplemente establezca su número aquí. Establezca vacío si debe usar la base de datos diferente para cada tipo de datos (usado por defecto). establezca -1 si desea utilizar la base de datos predeterminada.
* **RedisConnectionString:** Esta configuración espera un valor de cadena. El valor predeterminado para esta configuración es `127.0.0.1: {PUERTO}, ssl = Falso`. Aquí necesitamos establecer la "Cadena de conexión" para `Redis`. Se usa cuando Redis está habilitado.
* **UseRedisToStoreDataProtectionKeys:** Esta configuración espera un valor booleano. Esta configuración indica si el sistema de protección de datos debe configurarse para conservar las claves en la base de datos de Redis.
* **UseRedisForCaching:** Esta configuración espera un valor booleano. El sistema utiliza un almacenamiento en caché en memoria, por lo que esta configuración se usa para indicar si debemos usar el servidor `Redis` para el `almacenamiento en caché`, en lugar del `almacenamiento en memoria caché` predeterminado.Por lo tanto, use esta configuración si desea usar`Redis` para el `almacenamiento en caché`.
* **UseRedisToStorePluginsInfo:** Esta configuración espera un valor booleano. nopCommerce usa el archivo `plugin.json` para almacenar la información del plu. Entonces, esta configuración indica si debemos usar el servidor Redis para almacenar la información de los plus (en lugar del archivo plugin.json predeterminado).

#### Agente de usuario

En informática, un agente de usuario es un software (un agente de software) que actúa en nombre de un usuario, como un navegador web que "recupera, presenta y facilita la interacción del usuario final con el contenido web". Para mayor información por favor visite [UserAgent](https://en.wikipedia.org/wiki/User_agent)

* **UserAgentStringsPath:** Esta configuración almacena la ubicación / ruta para el archivo `Browscap.xml`,`Browscap.xml` es, como podría indicar el nombre del archivo, una base de datos de capacidades del navegador. Es esencialmente una lista de todos los navegadores y bots conocidos, junto con sus capacidades y limitaciones predeterminadas.
* **CrawlerOnlyUserAgentStringsPath:** Esta configuración almacena la ubicación / ruta de `browscap.crawlersonly.xml`. Almacena agentes de usuario solo para "CrawlerOnly"

#### Instalación

Contiene configuraciones que solían configurar el comportamiento de nopCommerce durante la instalación de nopCommerce.

* **DisableSampleDataDuringInstallation:** Esta configuración espera un valor booleano. Esta configuración indica si el propietario de una tienda puede instalar datos de muestra durante la instalación. Si no desea que el propietario de la tienda instale datos de muestra durante la instalación, simplemente establezca el valor de esta configuración en "**verdadero**".
* **UseFastInstallationService:** Esta configuración espera un valor booleano. De forma predeterminada, el valor de esta configuración es "**falso**". esta configuración indica si se debe utilizar la instalación rápida o no.
* **PluginsIgnoredDuringInstallation:** Esta configuración espera un valor booleano. De forma predeterminada, el valor de esta configuración es "**falso**". Es posible que desee establecer el valor de esta configuración en "**verdadero**" si no desea `Instalar` ningún `plu` durante la instalación de nopCommerce

#### Plugins

* **ClearPluginShadowDirectoryOnStartup:** Esta configuración espera un valor booleano. Es posible que desee establecer el valor en "**true**" si desea borrar el directorio `/ Plugins / bin` durante el inicio de la aplicación.
* **CopyLockedPluginAssembilesToSubdirectoriesOnStartup:** Esta configuración espera un valor booleano. Es posible que desee establecer el valor en "**true**" si desea copiar ensamblados "bloqueados" del directorio `/ Plugins / bin` a subdirectorios temporales durante el inicio de la aplicación.
* **UsePluginsShadowCopy:** Esta configuración espera un valor booleano. Es posible que desee establecer el valor en "**true**" si desea copiar la biblioteca de complementos al directorio `/ Plugins / bin` al iniciar la aplicación.
* **UseUnsafeLoadAssembly:** Esta configuración espera un valor booleano. Es posible que desee establecer el valor en "**true**" si desea cargar un ensamblado en el contexto de carga, omitiendo algunas comprobaciones de seguridad.

#### UseRowNumberForPaging

Esta configuración espera un valor booleano. El valor predeterminado para esta configuración es "**falso**". Es posible que desee establecer el valor en "**true**" si desea configurar su aplicación nopCommerce para que sea compatible con versiones anteriores de `SQL Server 2008`y `SQL Server 2008R2`.

#### UseSessionStateTempDataProvider

Esta configuración espera un valor booleano. El valor predeterminado para esta configuración es "**falso**". Es posible que desee establecer el valor en "**verdadero**" si desea almacenar `TempData` en el estado de la sesión. De forma predeterminada, el proveedor `TempData` basado en cookies se utiliza para almacenar `TempData` en las cookies.

### Clase NopConfig y HostingConfig

Como podemos ver, el archivo `appsettings.json` tiene muchas configuraciones definidas en él, que podemos usar en nuestra aplicación para que nuestra aplicación se comporte de acuerdo con la configuración definida en este archivo. Pero no queremos leer estas configuraciones del archivo `appsettings.json` cada vez que necesitamos acceder a estas configuraciones. Entonces, aquí es donde entran en juego las clases `NopConfig` y `HostingConfig`. Podemos encontrar estas clases en `Libraries / Nop.Core / Configuration`. Si abre estas clases, puede ver que las propiedades de estas clases son las mismas que las propiedades en el archivo `appsettings.json`.
si observa las propiedades de la clase `HostingConfig` y la configuración de `Host` en `appsetting.json` y la clase`NopConfig` y la configuración de `Nop` en el archivo`appsettings.json`, tienen las mismas propiedades. Esto se debe a que cargamos la configuración de `appsettings.json` a estos archivos y la inyectamos a los controladores mediante el mecanismo de inyección de dependencia.
