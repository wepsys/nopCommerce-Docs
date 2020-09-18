---
title: Adding a favicon
uid: en/getting-started/design-your-store/adding-a-favicon
author: git.RomanovM
contributors: git.rajupaladiya, git.DmitriyKulagin, git.mariannk
---

# Subir favicons

Desde la versión 4.20 puede cargar automáticamente favicons a través del área de administración.

> [!NOTE]
>
> Para el caso de varias tiendas, debe repetir este procedimiento de carga para cada tienda.

1. Para cargar favicons vaya a  **Configuración > Configuración > Ajustes generales.** Se muestra el panel *Iconos de favicon y aplicación*:  
![settings_block](_static/adding-a-favicon/settings_block.png)

1. Haga clic en el botón verde  **Cargar iconos archivo**, se abrirá el cuadro de diálogo de selección dearchivos: ![ file_selection_dialog](_static/adding-a-favicon/file_selection_dialog.png) Aquí es necesario copiar la ruta de acceso a sus iconos(varía depende de la tienda y el directorio virtual). Por ejemplo:  `/icons/icons_0`.

1. Hay varias opciones para qué cargar, dependiendo de lo amigable que sus favicons sitio deben ser para diferentes dispositivos:

- La opción más completa es utilizar uno de los generadores de favicon. En este manual, mostraremos un ejemplo del uso de un [RealFaviconGenerator](https://realfavicongenerator.net/). Gracias a este servicio, la carga del paquete favicon completo se llevará a cabo en unos pocos clics.

* Ir a esta página principal generador donde se le invitará a elegir una imagen para el favicon
![realfavicongenerator](_static/adding-a-favicon/realfavicongenerator.png)

* Después de seleccionar una imagen y hacer clic en  **Continuar con esta imagen**, será redirigido a la página siguiente. Aquí puede ajustar la configuración de pantalla de favicons para dispositivos y aplicaciones específicos - iOS Web Clip, Android Chrome, Windows Metro, macOS Safari, etc. El servicio mostrará automáticamente ejemplos de visualización. Puede personalizarlos según sus necesidades o dejar las predeterminadas.

* En la parte inferior de la misma página se puede encontrar el panel **Opciones del generador de Favicon**.  
![favicon_generator_options](_static/adding-a-favicon/favicon_generator_options.png)

- En esta sección, debe establecer ciertos ajustes. En la pestaña **Path**,  seleccione la opción  'No puedo o no quiero colocar archivos favicon en la raíz de mi sitio web. En su lugar, los colocaré aquí'  y especificaré la ruta desde el paso 2. ![ favicon_path](_static/adding-a-favicon/favicon_path.png)

- En la pestaña Versión/Actualizar,seleccione la opción en función de si su sitio ya está en producción. La descripción de la configuración le ayudará con esto. ![favicon_version](_static/adding-a-favicon/favicon_version.png)

- En la pestaña **Campos adicionales**  es necesario comprobar la opción para generar un archivo html en el paquete. ![ favicon_additional_fields](_static/adding-a-favicon/favicon_additional_fields.png)

* Ahora todos los ajustes están establecidos, haga clic en el botón para generar. ![generate_button](_static/adding-a-favicon/generate_button.png)

* Obtener su paquete favicon. ![download_package](_static/adding-a-favicon/download_package.png)

- La opción más simple es utilizar sólo el archivo favicon.ico,ico, que se ha utilizado con éxito en muchos sitios durante mucho tiempo, hasta que aparecieron dispositivos con diferentes resoluciones de pantalla.

* Encuentra un paquete favicon de muestra que se encuentra en el directorio `wwwroot/icons/samples/`  y cópialo.

* En el nuevo paquete, elimine todos los archivos excepto  **favicon.ico**  y  **html_code.html**.

* Reemplace en este paquete el archivo  **favicon.ico**  con su nuevo favicon.

* Edite el archivo **html_code.html**.  Deje la única línea allí:  `<link rel="icono de acceso directo" href="/icons/icons_0/favicon.ico">`,suponiendo que  `/icons/icons_0` es la ruta desde el paso 2.

* Guarde estos dos archivos en un paquete. Tu paquete favicon está listo.

- Una opción intermedia es utilizar el paquete favicon completo sin un generador.

1. Busque un paquete de favicon de muestra que se encuentre en el directorio `wwwroot/icons/samples/`  y cópielo.

1. Sustituya las imágenes del nuevo paquete por las suyas propias teniendo en cuenta los tamaños originales.

1. Edite el archivo **html_code.html**,  reemplace todas las entradas de  `wwwroot/icons/samples/`  por la ruta que se guardó en el paso 2.

1. Guarde este paquete. Tu paquete favicon está listo.

1. Vuelva al área de administración con un paquete favicon preparado para cargar. Seleccione el archivo deseado y haga clic en  **Cargar archivo de iconos**. ![ upload_package](_static/adding-a-favicon/file_selection_dialog.png)

1. Asegúrese de que su paquete se ha cargado correctamente. ![éxito](_static/adding-a-favicon/success.png)

1. Para ver el nuevo favicon en el sitio debe borrar la caché en el área de administración y en el navegador y luego volver a cargar la página.

> [!TIP]
>
> Para crear un paquete favicon, puede utilizar cualquier generador, servicio de terceros o hacerlo manualmente. El único requisito es la existencia del archivo **html_code.html**  con el código html, que se colocará en el elemento `<head>`  de las páginas del sitio.
