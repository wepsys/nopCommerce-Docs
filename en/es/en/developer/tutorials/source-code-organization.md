---
title: Source code organization. Architecture of nopCommerce.
uid: en/developer/tutorials/source-code-organization
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Organización del código fuente. Arquitectura de nopCommerce

Este documento es una guía para los desarrolladores de la estructura de la solución de nopCommerce. Es un documento para que un nuevo desarrollador de nopCommerce empiece a aprender sobre el código base de nopCommerce. En primer lugar, el código fuente de nopCommerce es bastante fácil de obtener. Es una aplicación de código abierto, así que todo lo que tienes que hacer para obtener el código es simplemente descargarlo del sitio web. Los proyectos y carpetas se listan en el orden en que aparecen en Visual Studio. Te recomendamos que abras la solución nopCommerce en Visual Studio y que navegues por los proyectos y archivos mientras lees este documento.

![Visual Studio](_static/source-code-organization/visual_studio.jpg)

La mayoría de los proyectos, directorios y archivos tienen nombres para que puedas tener una idea aproximada de su propósito. Por ejemplo, ni siquiera tengo que mirar dentro del proyecto llamado Nop.Plugin.Payments.PayPalStandard para adivinar lo que hace.

## `\Libraries\Nop.Core`

El proyecto Nop.Core contiene un conjunto de clases básicas para nopCommerce, tales como caché, eventos, ayudantes y objetos comerciales (por ejemplo, entidades de pedidos y clientes).

## `\Libraries\Nop.Data`

El proyecto Nop.Data contiene un conjunto de clases y funciones para leer y escribir en una base de datos u otro almacén de datos. Ayuda a separar la lógica de acceso a los datos de los objetos de su empresa. nopCommerce utiliza el enfoque de Entity Framework (EF) Code-First. Permite definir entidades en el código fuente (todas las entidades centrales se definen en el proyecto Nop.Core), y luego hacer que EF genere la base de datos a partir de ella. Por eso se llama Code-First. Puedes entonces consultar tus objetos usando LINQ, que se traduce a SQL entre bastidores y se ejecuta contra la base de datos. nopCommerces usa  [Fluent API](https://www.entityframeworktutorial.net/efcore/fluent-api-in-entity-framework-core.aspx) para personalizar completamente la cartografía de la persistencia.

## `\Libraries\Nop.Services`

Este proyecto contiene un conjunto de servicios básicos, lógica comercial, validaciones o cálculos relacionados con los datos, si es necesario. Algunas personas lo llaman Capa de Acceso al Negocio (BAL).

## Projects into `\Plugins\` solution folder

"Plugins" es una carpeta de soluciones de Visual Studio que contiene proyectos de plugins. Físicamente se encuentra en la raíz de tu solución. Pero las DLLs de los plugins se copian automáticamente en el directorio ``Presentation\Nop.Web\Plugins`` que se utiliza para los plugins ya desplegados porque las rutas de salida de la construcción de todos los plugins se establecen en `..\N..\NPresentation\NNNNNNNNNop.Web\NPlugins {Group}.{Nombre}`. Esto permite que los plugins contengan algunos archivos externos, como contenido estático (archivos CSS o JS) sin tener que copiar archivos entre proyectos para poder ejecutar el proyecto.

## `\Presentation\Nop.Web`

`Nop.Web` es un proyecto de aplicación web de MVC, una capa de presentación para la tienda pública que también contiene un panel de administración incluido como un área. Si no has usado `ASP.NET` antes, por favor encuentra más información [aquí](http://www.asp.net/). Esta es la aplicación que realmente ejecutas. Es el proyecto de inicio de la aplicación.

## `\Presentation\Nop.Web.Framework`

Nop.Web.El marco es un proyecto de biblioteca de la clase conteniendo algunas cosas de presentación comunes para `Nop.Proyecto de web.

## `\Test\Nop.Core.Tests`

Nop.Core.Tests es el proyecto de prueba del proyecto Nop.Core.

## `\Test\Nop.Services.Tests`

Nop.Services.Tests es el proyecto de prueba del proyecto Nop.Services.

## `\Test\Nop.Tests`

Nop.Tests es un proyecto de biblioteca de clases que contiene algunas clases de pruebas comunes y ayudantes para otros proyectos de pruebas. No tiene ningún test.

## `\Test\Nop.Web.MVC.Tests`

Nop.Web.MVC.Tests es el proyecto de prueba para los proyectos de capa de presentación.

## Tutorials

- [The Architecture behind the nopCommerce eCommerce Platform](https://www.youtube.com/watch?v=6gLbizzSA9o&list=PLnL_aDfmRHwtJmzeA7SxrpH3-XDY2ue0a)
