---
title: Instruction on how to start developing on nopCommerce
uid: en/developer/tutorials/instruction-on-how-to-start-developing-on-nopcommerce
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Instrucciones sobre cómo comenzar a desarrollar en nopCommerce 4.30

## Cosas cubiertas en este tutorial

1. Herramientas necesarias para el desarrollo.
2. Pila de tecnologías utilizadas en nopCommerce.
3. Instrucciones sobre cómo descargar el proyecto y ejecutarlo en la máquina local.
4. Cómo configurar nopCommerce para que se ejecute en HTTPS.

## Resumen

nopCommerce es una solución de comercio electrónico basada en Microsoft ASP.NET de código abierto. Esta es una guía básica para desarrolladores sobre cómo comenzar a desarrollar en nopCommerce.

## 1. Herramientas necesarias para el desarrollo

Puede obtener información sobre la tecnología y los requisitos del sistema en el **"[Herramientas necesarias para el desarrollo](xref:en/developer/tutorials/system-requirements-for-development#2-tools-required-for-development)"** artículo

## 2. Pila de tecnologías utilizadas en nopCommerce

La mejor parte de nopCommerce es que su código fuente es totalmente personalizable y su arquitectura conectable facilita el desarrollo de funciones personalizadas y el seguimiento de los requisitos comerciales mediante el uso del sistema de complementos. Sigue arquitecturas de software conocidas, patrones y las mejores prácticas de seguridad. Y, sobre todo, funciona con las últimas tecnologías para ofrecer la mejor experiencia posible a los usuarios finales. Entonces, para lograr todo esto, nopCommerce usa una pila de tecnologías en su arquitectura.

* Capa de aplicación
  * Motor Razor View

    Es para renderizar la página html en el lado del cliente. El motor Razor View es una sintaxis de marcado que nos ayuda a escribir código HTML y del lado del servidor en páginas web usando C # o VB.NET.
  * JQuery

    Es una biblioteca de JavaScript que se utiliza para ampliar la funcionalidad de UI y UX de las páginas html.
  * Interfaz de usuario de Kendo

    Kendo UI es un marco integral de interfaz de usuario HTML5 para crear sitios web y aplicaciones interactivos y de alto rendimiento

* Capa empresarial
  * Validación fluida

    Es una biblioteca de validación para .NET que utiliza una interfaz fluida y expresiones lambda para crear reglas de validación.
  * AutoMapper

    AutoMapper es una biblioteca simple que nos ayuda a transformar un tipo de objeto en otro. Es un mapeador objeto a objeto basado en convenciones que requiere muy poca configuración.
  * AutoFac

    Autofac es un contenedor de IoC adictivo para .NET. Gestiona las dependencias entre clases para que las aplicaciones sean fáciles de cambiar a medida que crecen en tamaño y complejidad.
  * Linq2DB

    Linq2DB es un marco ORM de código abierto para aplicaciones .NET. Es un proyecto de .NET Foundation. Permite a los desarrolladores trabajar con datos utilizando objetos de clases específicas de dominio sin centrarse en las tablas y columnas de la base de datos subyacente donde se almacenan estos datos. Por lo tanto, es el puente entre la capa empresarial y la capa de datos.
  * FluentMigrator

    Fluent Migrator es un marco de migración para .NET. Las migraciones son una forma estructurada de alterar el esquema de su base de datos y son una alternativa a la creación de muchos scripts SQL que todos los desarrolladores involucrados deben ejecutar manualmente. Las migraciones resuelven el problema de desarrollar un esquema de base de datos para múltiples bases de datos (por ejemplo, la base de datos local del desarrollador, la base de datos de prueba y la base de datos de producción). Los cambios en el esquema de la base de datos se describen en clases escritas en C # que se pueden registrar en un sistema de control de versiones.
* Capa de datos
  * Microsoft SQL Server

    SQL Server es el sistema de administración de bases de datos relacionales (RDBMS) con todas las funciones de Microsoft.
  * Servidor MySQL

    MySQL es la base de datos de código abierto más popular del mundo. Con su rendimiento, confiabilidad y facilidad de uso comprobados, MySQL se ha convertido en la principal opción de base de datos para aplicaciones basadas en web.
  * Redis (caché)

    Redis es un almacén de estructura de datos en memoria de código abierto (licencia BSD) que se utiliza como base de datos, caché y agente de mensajes. Entonces, en nopCommerce Redis se usa para almacenar datos antiguos como un conjunto de datos de caché en memoria. Lo que aumenta la velocidad y el rendimiento de la aplicación.
  * Microsoft Azure (opcional)

    Azure es una plataforma de computación en la nube pública con soluciones que incluyen infraestructura como servicio (IaaS), plataforma como servicio (PaaS) y software como servicio (SaaS) que se puede utilizar para servicios como análisis, computación virtual, almacenamiento, redes. , y mucho más.

## 3. Cómo descargar el proyecto y ejecutarlo en la máquina local

Antes de comenzar a trabajar con nopCommerce, debemos asegurarnos de que nuestra máquina local esté configurada y debemos asegurarnos de que todas nuestras herramientas necesarias para desarrollar en nopCommerce estén instaladas y funcionando correctamente. Ahora, vayamos a las instrucciones paso a paso sobre cómo descargar y ejecutar nopCommerce en nuestra máquina local.

### Paso 1: Descarga el código fuente de nopCommerce

Para descargar, visite [este sitio](https://www.nopcommerce.com/download-nopcommerce). Allí puede ver dos botones de descarga, uno con un código fuente y otro sin código fuente, como se muestra en la siguiente imagen.

![image1] (_estática/instrucción-sobre-cómo-empezar-a-desarrollar-en-nopcommerce/image1.png)

Ya que estamos descargando nopCommerce para propósitos de desarrollo, necesitamos descargar el que dice "Paquete con código fuente" que contiene todo el código fuente de nopCommerce. En orden
