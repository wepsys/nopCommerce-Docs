---
title: Overview (Designer's Guide)
uid: en/developer/design/overview
author: git.AndreiMaz
contributors: git.exileDev, git.DmitriyKulagin
---

# Descripción general (guía del diseñador)
## Qué es un tema

Un tema es una colección de configuraciones de propiedades que le permiten definir el aspecto de las páginas y los controles, y luego aplicar el aspecto de manera coherente en las páginas de una aplicación web, en toda una aplicación web o en todas las aplicaciones web de un servidor.

Los temas se componen de un conjunto de elementos: máscaras, hojas de estilo en cascada (CSS), imágenes y otros recursos. Como mínimo, un tema contendrá máscaras. Los temas se definen en directorios especiales en su sitio web o en su servidor web.

Un tema también puede incluir una hoja de estilo en cascada (archivo `.CSS`). Cuando coloca un archivo `.CSS` en la carpeta del tema, la hoja de estilo se aplica automáticamente como parte del tema. Usted define una hoja de estilo usando la extensión de nombre de archivo `.CSS` en la carpeta del tema. (Fuente: [msdn.microsoft.com](https://msdn.microsoft.com))

## Definición de un tema nopCommerce

Un tema nopCommerce se usa básicamente para tener un diseño y una apariencia consistentes en todas las páginas o en un sitio web completo. El tema nopCommerce consta de varios archivos de apoyo, incluidas hojas de estilo para la apariencia de la página e imágenes de apoyo.

![location-of-themes](_static/overview/location-of-themes.png)

**Ubicación de los temas en nopCommerce**: Todos los temas se encuentran en `[carpeta raíz de nopCommerce]/Themes/`.