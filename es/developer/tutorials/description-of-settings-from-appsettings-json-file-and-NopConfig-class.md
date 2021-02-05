---
title: Description settings from appsettings.json file and NopConfig and HostingConfig class
uid: es/developer/tutorials/description-of-settings-from-appsettings-json-file-and-NopConfig-class
author: git.nopsg
contributors: git.nopsg, git.DmitriyKulagin
---

# Descripción de la configuración del archivo appsettings.json y la clase NopConfig y HostingConfig

## Visión general

Este artículo contiene una descripción del archivo `appsettings.json` y la `clase NopConfig`. En este artículo explicaremos cuáles son las diferentes configuraciones disponibles en estos archivos, qué hace cada configuración y cuándo usar esta configuración para cambiar la funcionalidad/comportamiento del proyecto nopCommerce.

## descripción general del archivo appsettings.json

Si ha trabajado en el proyecto `ASP.NET core` anteriormente o está familiarizado con el `ASP.NET core`, entonces es posible que haya usado el archivo `appsettings.json` y tenga algún conocimiento de qué es este archivo y para qué se usa. para.

El archivo `appsettings.json` se usa generalmente para almacenar los ajustes de configuración de la aplicación, como las cadenas de conexión de la base de datos, las variables globales del alcance de la aplicación y mucha otra información. En realidad, en `ASP.NET Core`, los ajustes de configuración de la aplicación se pueden almacenar en diferentes fuentes de configuración, como el archivo `appsettings.json`, el archivo `appsettings. {EnvironmentName}.json` (donde{Environment} es el alojamiento actual de la aplicación entornos como Desarrollo, Puesta en escena o Producción), `Secretos de usuario` (donde solíamos almacenar información confidencial), etc.

## Configuraciones disponibles en el archivo appsettings.json

### Alojamiento

El alojamiento contiene la configuración que se utiliza para configurar el comportamiento del alojamiento. Es un objeto json y contiene algunas configuraciones de propiedades que se pueden modificar para cambiar el comportamiento del alojamiento.

#### UseHttpClusterHttps

Esta configuración espera un valor booleano. El valor predeterminado es "**falso**", puede establecer el valor en "**verdadero**" si su alojamiento utiliza un equilibrador de carga. Se utilizará para determinar si la solicitud actual es HTTPS.

#### UseHttpXForderedProto

Esta configuración espera un valor booleano. El valor predeterminado es "**falso**". Es posible que desee establecer el valor en "**verdadero**" si su alojamiento utiliza un equilibrador de carga y si está habilitando la configuración **`UseHttpClusterHttps`** anterior. Esta configuración se usa para agregar **`X-Fordered-Proto`** en el encabezado `HTTP`. **`X-Fordered-Proto`** es un encabezado HTTP y es parte del estándar HTTP. Se establece en cada solicitud HTTP por un proxy o equilibrador de carga y puede ser utilizado por una aplicación de servidor para determinar qué protocolo utilizó el cliente para conectarse.

#### ForderedHttpHeader

Esta configuración espera un valor de cadena. Puede utilizar esta configuración si su alojamiento no utiliza el encabezado 
""X-FORWARDED-FOR"` para determinar la dirección IP. En algunos casos, el servidor utiliza otro encabezado HTTP. Puede especificar un encabezado HTTP personalizado aquí. Por ejemplo, CF-Connecting-IP, X-FORWARDED-PROTO, etc.

### Nop

Nop contiene ajustes que se utilizan para configurar el comportamiento de nopCommerce. Es un objeto json y contiene algunas configuraciones de propiedades que se pueden modificar para cambiar el comportamiento de nopCommerce.

#### DisplayFullErrorStack

Esta configuración espera un valor booleano. El valor predeterminado es **"falso"**. Puede establecer el valor en "**verdadero**" si desea ver el error completo en el entorno de producción. Que no es lo que solemos sugerir. Pero si tiene una buena razón para mostrar un error completo durante el entorno de producción, puede hacerlo desde esta configuración. Para el entorno de desarrollo, esta configuración se ignora y cualquiera que sea el valor que establezca para esta configuración, se mostrará el error completo. Podemos decir que esta configuración siempre está habilitada para el entorno de desarrollo.

#### Azure Blob Storage

Podemos usar "Azure Blob Storage" para almacenar datos de blobs. nopCommerce ya tiene una función integrada para eso, solo necesitamos configurar la siguiente información correctamente para usar/habilitar esta función. Los valores de esta configuración se pueden obtener para Azure mientras crea la cuenta de almacenamiento.

* **AzureBlobStorageConnectionString:** Esta configuración espera un valor de cadena. Aquí debe agregar su cadena de conexión `AzureBlobStorage`
* **AzureBlobStorageContainerName:** El valor de esta configuración también es de tipo cadena. En esta configuración, establecemos el nombre del contenedor para el almacenamiento de Azure BLOB.
* **AzureBlobStorageEndPoint:** Esta configuración también espera un valor de cadena. Aquí tenemos que establecer el punto final para el almacenamiento de Azure BLOB.
* **AzureBlobStorageAppendContainerName:** Esta configuración espera un valor booleano. Establezca el valor en "**verdadero**" o "**falso**" en función de si el nombre del contenedor se agrega al `AzureBlobStorageEndPoint` al construir la URL.

#### Redis

nopCommerce admite *Redis* listo para usar. Para habilitar el `Redis` en nuestra aplicación, debemos establecer el valor apropiado para las siguientes configuraciones. Para obtener más información sobre [Redis](https://azure.microsoft.com/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache).

* **RedisEnabled:** Esta configuración espera un valor booleano. Establezca el valor en **"verdadero"** si desea habilitar `Redis`.
* **RedisDatabaseId:** ID de la base de datos de Redis. Si necesita utilizar una base de datos de Redis específica, simplemente establezca su número aquí. Establezca vacío si debe usar la base de datos diferente para cada tipo de datos (usado por defecto). establezca -1 si desea utilizar la base de datos predeterminada.
* **RedisConnectionString:**
