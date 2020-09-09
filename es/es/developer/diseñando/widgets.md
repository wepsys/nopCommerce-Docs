---
title: Widgets (Designer's Guide)
uid: en/developer/design/widgets
author: git.AndreiMaz
contributors: git.exileDev, git.DmitriyKulagin
---

# Widgets (Guía del diseñador)

> Un widget es una aplicación independiente que cualquier usuario de una página puede incrustar en sitios de terceros. Es una pequeña aplicación que un usuario final puede instalar y ejecutar dentro de una página web. (Wikipedia).

En nopCommerce, un complemento de widget le permite incrustar código / aplicación de terceros en la tienda pública en ciertas áreas (por ejemplo, etiqueta de cabeza, etiqueta después del cuerpo, bloque de columna izquierda y bloque de columna derecha).

Actualmente, la instalación predeterminada de nopCommerce permite al administrador de la tienda incrustar dos complementos de widgets:

1. Google Analytics
1. Control deslizante Nivo

##Widget de Google Analytics

Google Analytics es una herramienta gratuita de estadísticas de sitios web de Google. Realiza un seguimiento de las estadísticas sobre los visitantes y la conversión de comercio electrónico en su sitio web. Este bloque de widgets se puede representar en:

* Etiqueta de encabezado HTML
* Después de la etiqueta HTML final `<body>`.

Para configurar el widget de Google Analytics, vaya a `Administración → Configuración → Widgets`, haga clic en ** Configurar ** contra ** Google Analytics ** y agregue su código de Google Analytics.

## Control deslizante Nivo

El control deslizante de Nivo es un control deslizante de imágenes jquery agradable y limpio para su sitio web/página de inicio para mostrar una serie de imágenes que se desplazan con efectos de transición únicos.

De forma predeterminada, nopCommerce viene con la integración del control deslizante nivo como un widget (habilitado de forma predeterminada) que le permite mostrar una serie de imágenes que se desplazan automáticamente en su página de inicio.