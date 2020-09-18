---
title: Instruction on how to start developing on nopCommerce
uid: en/developer/tutorials/instruction-on-how-to-start-developing-on-nopcommerce
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Instrucción sobre cómo empezar a desarrollar el nopCommerce 4.30

## Cosas cubiertas en este tutorial

1. Herramientas necesarias para el desarrollo.
2. Pila de tecnologías utilizadas en nopCommerce.
3. Instrucciones para descargar el proyecto y ejecutarlo en la máquina local.
4. Cómo configurar nopCommerce para que funcione con HTTPS.

## Resumen

nopCommerce es una solución de comercio electrónico de código abierto basada en Microsoft ASP.NET. Esta es una guía básica para los desarrolladores sobre cómo empezar a desarrollar en nopCommerce.

## 1. Herramientas necesarias para el desarrollo

Puedes aprender sobre la tecnología y los requisitos del sistema en el **"[Tools Required for Development](xref:en/developer/tutorials/system-requirements-for-developing#2-tools-required-for-development)"** article

## 2. La pila de tecnologías utilizadas en nopCommerce

Lo mejor de nopCommerce es que su código fuente es totalmente personalizable y su arquitectura enchufable facilita el desarrollo de funcionalidades personalizadas y el seguimiento de cualquier requisito empresarial mediante el uso de un sistema de plugin. Sigue arquitecturas de software bien conocidas, patrones y las mejores prácticas de seguridad. Y sobre todo, funciona con las últimas tecnologías para ofrecer la mejor experiencia posible a los usuarios finales. Así que, para lograr todo esto nopCommerce utiliza una pila de tecnologías en su arquitectura.

* Capa de aplicación
  * Razor View Engine

    Es para renderizar la página html en el lado del cliente. El motor de Razor View es una sintaxis de marcado que nos ayuda a escribir HTML y código del lado del servidor en páginas web usando C# o VB.NET.
  * JQuery

    Es una biblioteca de javascript utilizada para extender la funcionalidad de UI & UX de las páginas html.
  * Kendo UI

    La interfaz de usuario de Kendo es un marco completo de interfaz de usuario HTML5 para construir sitios web y aplicaciones interactivas y de alto rendimiento

* Capa de negocios
  * Validación fluida

    Es una biblioteca de validación para .NET que utiliza una interfaz fluida y expresiones lambda para construir reglas de validación.
  * AutoMapper

    AutoMapper es una simple biblioteca que nos ayuda a transformar un tipo de objeto en otro. Es un mapeador convencional de objeto a objeto que requiere muy poca configuración.
  * AutoFac

    El Autofac es un contenedor de IO adictivo para el .NET. Maneja las dependencias entre clases para que las aplicaciones sean fáciles de cambiar a medida que crecen en tamaño y complejidad.
  * Linq2DB

    Linq2DB es un marco ORM de código abierto para aplicaciones .NET. Es un proyecto de la Fundación .NET. Permite a los desarrolladores trabajar con datos utilizando objetos de clases específicas del dominio sin centrarse en las tablas y columnas de la base de datos subyacentes donde se almacenan estos datos. Por lo tanto, es el puente entre la capa de negocios y la capa de datos.
  * FluentMigrator

    Fluent Migrator es un marco de migración para .NET. Las migraciones son una forma estructurada de alterar el esquema de la base de datos y son una alternativa a la creación de muchos scripts sql que tienen que ser ejecutados manualmente por cada desarrollador involucrado. Las migraciones resuelven el problema de la evolución de un esquema de base de datos para múltiples bases de datos (por ejemplo, la base de datos local del desarrollador, la base de datos de prueba y la base de datos de producción). Los cambios en el esquema de la base de datos se describen en clases escritas en C# que se pueden comprobar en un sistema de control de versiones.
* Capa de datos
  * Microsoft SQL Server

    SQL Server es el sistema de gestión de bases de datos relacionales de Microsoft con todas las funciones (RDBMS).
  * Servidor MySQL

    MySQL es la base de datos de código abierto más popular del mundo. Con su probado rendimiento, fiabilidad y facilidad de uso, MySQL se ha convertido en la principal base de datos para aplicaciones basadas en la web.
  * Redis (caché)

    Redis es un almacén de estructura de datos en memoria de código abierto (con licencia BSD), utilizado como base de datos, caché y agente de mensajes. Así que, en nopCommerce Redis se utiliza para almacenar datos antiguos como conjunto de datos en la memoria caché. Lo que aumenta la velocidad y el rendimiento de la aplicación.
  * Microsoft Azure(Opcional)

    Azure es una plataforma pública de computación en nube con soluciones que incluyen Infraestructura como un Servicio (IaaS), Plataforma como un Servicio (PaaS) y Software como un Servicio (SaaS) que puede ser utilizada para servicios tales como análisis, computación virtual, almacenamiento, redes y mucho más. 

## 3. Cómo descargar el proyecto y ejecutarlo en la máquina local

Antes de empezar a trabajar con nopCommerce necesitamos asegurarnos de que nuestra máquina local está configurada y necesitamos asegurarnos de que todas nuestras herramientas necesarias para desarrollar en nopCommerce están instaladas correctamente y funcionan correctamente. Ahora, vayamos a las instrucciones paso a paso sobre cómo descargar y ejecutar nopCommerce en nuestra máquina local.

### Paso 1: Descargar el código fuente de nopCommerce

Para descargarlo, por favor visite [este sitio](https://www.nopcommerce.com/download-nopcommerce). Allí puede ver dos botones de descarga, uno con un código fuente y otro sin código fuente como se muestra en la imagen de abajo.

![image1](_static/instruction-on-how-to-start-developing-on-nopcommerce/image1.png)

Ya que estamos descargando nopCommerce con fines de desarrollo, necesitamos descargar el que dice "Paquete con código fuente" que contiene todo el código fuente de nopCommerce. Para poder descargar nopCommerce es necesario iniciar sesión o registrar una nueva cuenta. Ahora puedes descargar nopCommerce como un archivo RAR, y extraerlo a la ubicación de la carpeta deseada.

### Paso 2: Abrir la solución nopCommerce en Visual Studio

Abre la carpeta, dentro de esa carpeta verás un montón de archivos y carpetas que contienen todo el código fuente de nopCommerce.

![image2](_static/instruction-on-how-to-start-developing-on-nopcommerce/image2.png)

Allí también verás un archivo de solución con la extensión `.sln`, por favor, haz doble clic en ese archivo de solución para abrir el proyecto nopCommerce en tu Visual Studio.

### Paso 3: Ejecutar el proyecto nopCommerce usando Visual Studio

nopCommerce no requiere de ninguna otra configuración para ejecutar el proyecto. nopCommerce está listo para salir de la caja. Por lo tanto, ahora puedes ejecutar el proyecto utilizando Visual Studio pulsando ctrl+F5 o sólo F5 para ejecutar el proyecto en modo de depuración, o puedes ejecutarlo utilizando el botón físico con el icono de reproducción en Visual Studio. Después de ejecutar el proyecto por primera vez, verás una página de instalación como la que se muestra a continuación:

![image3](_static/instruction-on-how-to-start-developing-on-nopcommerce/nop_install.jpg)

Aquí tienes que rellenar toda la información necesaria para completar tu instalación.

#### Información de la tienda

Aquí se requiere una dirección de correo electrónico y una contraseña que luego se utiliza como cuenta de administrador en su tienda nopCommerce.

#### Información de la base de datos

Aquí tienes que proporcionar la información que quieres usar para este proyecto.

Aquí tienes dos elegir tu almacenamiento de base de datos. Puedes usar MS SQL Server o MySQL server. Es tu decisión cuál quieres usar.

En este tutorial utilizaremos el MS SQL Server.

También verás la casilla de verificación que te preguntará si quieres crear una base de datos si no existe, por favor marca la casilla.

Avanzando un poco más, necesita configurar su cadena de conexión. Para ello, tienes dos opciones. Una es llenar el formulario con "Nombre del servidor SQL" y "Nombre de la base de datos". En el nombre del servidor SQL tienes que proporcionar el nombre de tu servidor SQL y en el nombre de la base de datos tienes que proporcionar el nombre de la base de datos que quieres crear o si ya tienes una entonces no creará sino que utilizará la existente. Sin embargo, también puede elegir la opción "Introducir cadena de conexión en bruto", entonces usted necesita escribir toda la cadena de conexión por sí mismo. Después de eso usted necesita proporcionar las credenciales de su servidor SQL para la autenticación.

Después de rellenar toda esta información, debe pulsar el botón "instalar", le llevará aproximadamente 1 minuto completar la instalación, y luego será redirigido a la página de inicio de la tienda online.

### 4. Cómo configurar nopCommerce para que funcione con HTTPS

Para establecer SSL/HTTPS para tu nopCommerce necesitas ir a la ventana de propiedades del proyecto `Nop.Web` en la carpeta de presentación ya que es el proyecto de inicio de nopCommerce. Para abrir la ventana de propiedades haz click con el botón derecho del ratón sobre el proyecto `Nop.Web` y en la parte inferior del menú contextual verás un menú llamado "Properties", simplemente haz click en ese menú y aparecerá una ventana de propiedades. En la ventana de propiedades navega a la pestaña "Debug".

![image4](_static/instruction-on-how-to-start-developing-on-nopcommerce/image4.png)

Marque la casilla "Activar SSL", e introduzca la URL HTTPS al lado. Luego guarda este proyecto.

Ahora ejecuta tu proyecto de nuevo y navega a la URL dada y puedes ver que ahora se está ejecutando en SSL/HTTPS. Así que esta es la única manera de configurar HTTPS en tu proyecto web, pero también hay otra manera de configurar SSL. Para eso ve a tu proyecto `Nop.Web` y expande el proyecto dentro de allí verás un archivo virtual llamado "Propiedades" en tu estructura de proyecto justo debajo de "Dependencias". Dentro de "Propiedades" encontrarás un archivo JSON llamado launchSetting.json. Abre ese archivo y verás un montón de ajustes de configuración ya escritos en ese archivo.

Dentro de ese archivo puedes tener una sección como la que se muestra en la figura de arriba. Así que para habilitar SSL sólo necesitas reemplazar el 0 en la propiedad "sslPort" al puerto que quieres ejecutar para la conexión SSL, asegúrate de que el puerto esté disponible. Para probar, ejecuta tu proyecto y navega a `https://localhost:yourport`.
