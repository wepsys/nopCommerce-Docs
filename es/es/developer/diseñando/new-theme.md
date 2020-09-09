---
title: Creating / Writing your own theme (using current / default theme)
uid: en/developer/design/new-theme
author: git.AndreiMaz
contributors: git.a-patel, git.exileDev, git.DmitriyKulagin
---

# Crear/escribir su propio tema (usando el tema actual/predeterminado)
Abra su solución o sitio web nopCommerce (versión web) en Visual Studio - Vaya a esta ubicación:

* Si usa código fuente: `\Nop.Web\Themes\`
* Si usa código fuente: `\[Project Root]\Themes\`

1. Seleccione cualquier tema predeterminado / actual
    ![paso 1](_static/new-theme/new-theme-step-1.jpg)

1. Ahora, haga clic derecho en el tema → seleccione COPIA

    ![paso-2] (_static/new-theme/new-theme-step-2.jpg)

1. Ahora seleccione lacarpeta "Tema" → haga clic derecho → PEGAR

    ![paso-3] (_tatic/new-theme/new-theme-step-3.jpg)

1. Obtendrá algo como "Copia del tema predeterminado/actual"

    ![paso-4] (_static/new-theme/new-theme-step-4.jpg)

1. Cambie el nombre, como quiera que sea el nombre de su nuevo tema. Por ejemplo, digamos: MyFirstTheme

    ![paso-5] (_static/new-theme/new-theme-step-5.jpg)

1. Ahora dentro de la carpeta de temas nuevos "MyFirstTheme" → abra `theme.json`

    ![paso-6] (_static/new-theme/new-theme-step-6.jpg)

1. Cambie el nombre del tema actual/existente con su nuevo nombre de tema "MyFirstTheme"

    ![paso-7] (_static/new-theme/new-theme-step-7.jpg)

1. Ahora, dentro de su nueva carpeta de temas "MyFirstTheme" → Contenido → Imágenes, agregue sus nuevas imágenes en el directorio "images" y comience a actualizar/personalizar su `style.css` de acuerdo con sus requisitos.

    Si desea probar los cambios → Vaya a la sección Administración → Aplique su nuevo tema → Guarde el cambio y obtenga una vista previa de su tienda pública.

    ![paso-8] (_static/new-theme/new-theme-step-8.jpg)