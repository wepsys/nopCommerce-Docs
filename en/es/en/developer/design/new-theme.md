---
title: Creating / Writing your own theme (using current / default theme)
uid: en/developer/design/new-theme
author: git.AndreiMaz
contributors: git.a-patel, git.exileDev, git.DmitriyKulagin
---

# Crear/Escribir su propio tema (usando el tema actual/predeterminado)

Abra la solución nopCommerce o el sitio web (versión web) en Visual Studio - Vaya a esta ubicación:

* Si se utiliza el código fuente:  ''Nop.Web'Temas'
* Si se utiliza la versión web:  ''[Raíz del proyecto]'Temas'

1. Seleccione cualquier tema predeterminado / actual

![step-1](_static/new-theme/new-theme-step-1.jpg)

1. Ahora, haga clic con el botón derecho en el tema , seleccione COPY

![step-2](_static/new-theme/new-theme-step-2.jpg)

1. Ahora seleccione la carpeta "Tema" - haga clic con el botón derecho en PASTE

![paso-3](_static/new-theme/new-theme-step-3.jpg)

1. Obtendrá algo como "Copia del tema predeterminado / actual"

![paso-4](_static/new-theme/new-theme-step-4.jpg)

1. Renombrarlo - lo que quieras para ser el nombre de tu nuevo tema – Por una instancia, digamos: MyFirstTheme

![step-5](_static/new-theme/new-theme-step-5.jpg)

1. Ahora, dentro de su carpeta de tema "MyFirstTheme" - abrir  'theme.json'

![step-6](_static/new-theme/new-theme-step-6.jpg)

1. Cambie el nombre del tema actual / existente con su nuevo nombre de tema "MyFirstTheme"

![step-7](_static/new-theme/new-theme-step-7.jpg)

1. Ahora, dentro de su nueva carpeta de temas "MyFirstTheme" - Contenido - Imágenes añadir sus nuevas imágenes en el directorio "imágenes" y empezar a actualizar/personalizar su 'style.css'  de acuerdo con sus requisitos.

Si desea probar los cambios , vaya a la sección De administrador > Aplicar el nuevo tema > Guardar cambio y obtener una vista previa de la tienda pública.

![paso-8](_static/new-theme/new-theme-step-8.jpg)
