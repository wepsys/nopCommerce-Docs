---
title: Upgrading nopCommerce
uid: es/installation-and-upgrading/upgrading-nopcommerce
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.rajupaladiya, git.exileDev, git.dunaenko
---

# Actualización de nopCommerce

Este capítulo describe cómo actualizar nopCommerce a la versión [más reciente](https://www.nopcommerce.com/download-nopcommerce). Es posible que desee hacer esto porque ha visto un mensaje en la sección de noticias de nopCommerce de su panel de control que le indica que hay una nueva versión disponible. nopCommerce no admite actualizaciones automáticas, debe hacerlo manualmente.

Siga los siguientes pasos:

1. Haga una copia de seguridad de todo en su sitio, incluida la base de datos. Esto es extremadamente importante para que pueda volver a un sitio en ejecución sin importar lo que suceda durante la migración.
1. Luego debe ejecutar los scripts de actualización de SQL. Tienes que ejecutarlos paso a paso. Por ejemplo, si su versión actual es 3.90 y la última versión disponible es 4.20, entonces debe actualizar a 4.00, luego a 4.10 y luego a 4.20. Así que descargue los scripts de actualización necesarios de nuestra página [descargar nopCommerce](https://www.nopcommerce.com/download-nopcommerce). Una vez descargado un script de actualización, ejecútelo en su base de datos.
1. Elimine todos los archivos de la versión anterior (todos excepto`App_Data\Settings.txt` y `App_Data\InstalledPlugins.txt`).
1. Cargue los archivos del nuevo sitio (obtenga la última versión [aquí](https://www.nopcommerce.com/download-nopcommerce)).
1. Cambie el nombre del archivo `setting.txt` a `dataSettings.json` y `InstalledPlugins.txt` a `plugins.json` (para 4.00 y 4.10, cambie el nombre de `InstalledPlugins.txt` a `installedPlugins.json`) y actualice el contenido con estructura json.
1. Asegúrese de que todo esté bien.

> [!NOTE]
>
> A medida que implementa, asegúrese de que los archivos de destino `Settings.txt` (o `dataSettings.json`) e `InstalledPlugins.txt` (o `plugins.json`) se actualicen según la última versión de nopCommerce, de modo que la producción El sitio continúa apuntando a la base de datos de producción.

> [!NOTE]
> Si almacenó sus imágenes en el sistema de archivos, haga una copia de seguridad de ellas (`\wwwroot\Images\`) y cópielas nuevamente después de la actualización.

> [!NOTE]
> **(actualización de 3.X a 4.X)**: Si desea actualizar desde una versión 3.90 a la última versión, primero debe instalar 4.00 (sobre la base de datos existente), ejecutar 3.90 a 4.00 script SQL de migración, y luego actualice a 4.10, 4.20, etc.

## Solución de problemas

Si tiene problemas después de la actualización, siempre puede restaurar su copia de seguridad y reemplazar los archivos por otros de su versión anterior. Siempre puede publicar una pregunta en nuestros [foros](https://www.nopcommerce.com/boards/).

> [!NOTE]
>
> Si al hacer una búsqueda avanzada en nuestros foros no puede encontrar lo que necesita, intente una búsqueda de Google centrada en el sitio nopCommerce: [sus palabras de búsqueda **sitio: [nopcommerce.com](https://www.nopcommerce.com/"nopcommerce.com")**].
