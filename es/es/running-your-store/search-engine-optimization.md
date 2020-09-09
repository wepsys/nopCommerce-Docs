---
title: Search engine optimization
uid: en/running-your-store/search-engine-optimization
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Optimización de motores de búsqueda

SEO significa optimización de motores de búsqueda, es un proceso para obtener tráfico de resultados de búsqueda "gratuitos", "orgánicos", "editoriales" o "naturales" en los motores de búsqueda. Todos los motores de búsqueda principales tienen resultados de búsqueda primarios, donde las páginas web y otro contenido como videos o listados locales se muestran y clasifican según lo que un motor de búsqueda considera más relevante para los usuarios.

nopCommerce admite técnicas de SEO para diferentes tipos de páginas en su tienda. Encuentre una lista de ellos en la sección [Ver-también](# ver-también).

## Configuración de SEO

Hay algunas configuraciones generales de SEO en nopCommerce, que se pueden aplicar a toda la tienda.

Para editar la configuración de SEO, vaya a **Configuración → Configuración → Configuración general**.

![Configuración de SEO](_static/search-engine-optimization/seo1.png)

* En el campo **Título predeterminado**, ingrese el título predeterminado para las páginas de su tienda.
* En el campo **Ajuste de SEO del título de la página**, seleccione el ajuste de SEO del título de la página requerido, de la siguiente manera:

  * El nombre de una página viene después del nombre de una tienda en el título:
  `YOURSTORE.COM` | PAGENAME

  * A store name comes after a page name in the title:
  PAGENAME | `YOURSTORE.COM`

* Especifique el **separador de título de página**.
* Ingrese las **meta palabras clave predeterminadas** para las páginas de su tienda. Esto se puede anular para categorías individuales, fabricantes, productos y algunas otras páginas.
* Ingrese la **meta descripción predeterminada** para las páginas de su tienda. Esto se puede anular para categorías individuales, fabricantes y productos y algunas otras páginas.
* Seleccione **Generar descripción META del producto**, para generar automáticamente las descripciones META del producto (si no se especifica en la página de detalles del producto) según la descripción breve del producto.
* Elija el **requisito de prefijo WWW**. Por ejemplo, `http://yourStore.com /` podría redirigirse automáticamente a `http://www.yourStore.com/`. Selecciona una de las siguientes opciones:
    * *No importa*
    * *Las páginas deben tener el prefijo WWW*
    * *Las páginas no deben tener prefijo WWW*
* Seleccione la casilla de verificación **Convertir caracteres no occidentales** para eliminar el acento en los nombres de SEO. Por ejemplo, convierta é en e.
* Seleccione la casilla de verificación **Habilitar URL canónicas** para transformar una URL en una URL canónica para permitir determinar si dos URL sintácticamente diferentes pueden conducir a una página con el contenido equivalente.
* Marque la casilla de verificación **Etiquetas META de Twitter** para generar etiquetas META de Twitter en la página de detalles del producto.
* Marque la casilla de verificación **Etiquetas META de Open Graph** para generar etiquetas META de Open Graph en la página de detalles del producto.
* Marque la casilla de verificación **Etiquetas de microdatos** para generar etiquetas de microdatos en la página de detalles del producto.
* Ingrese a **Personalizado &#60;head&#62; etiqueta**.Por ejemplo, algunos personalizados &#60;meta&#62; etiqueta. O déjelo en blanco si ignora esta configuración.

## Paneles SEO

Hay varios tipos de páginas en nopCommerce para las que puede configurar configuraciones de SEO individuales, incluidas meta palabras clave, meta descripción, meta título y nombres de páginas amigables para los motores de búsqueda. Esto se hace en los paneles de SEO de las secciones correspondientes del área de administración.

![Panel de SEO](_static/search-engine-optimization/seo-panel.jpg)

* En el campo **Nombre de página amigable para motores de búsqueda**, ingrese el nombre de la página utilizada por los motores de búsqueda. Si no ingresa nada, la URL de la página web se forma con el nombre de la página. Si ingresa *custom-seo-page-name*, se utilizará la siguiente URL personalizada: `http://www.yourStore.com/custom-seo-page-name`.

* En el campo **Meta título**, ingrese el título requerido. La etiqueta de título especifica el título de su página web. Lo recuperan los navegadores web y también lo utilizan los motores de búsqueda como Google para mostrar una página web en los resultados de búsqueda:
  ! [Meta título] (_static/search-engine-optimization/meta-title.jpg)

* Ingrese las **Meta palabras clave** requeridas. Describen el contenido de una página web de forma breve y concisa y, por lo tanto, son indicadores importantes del contenido de un sitio web para los motores de búsqueda. Las meta palabras clave ayudan a indicar a los motores de búsqueda cuál es el tema de la página. Las palabras clave generalmente se escriben en minúsculas.

* En el campo **Meta descripción**, ingrese una descripción de la página. La meta descripción proporciona un resumen de una página web. Los motores de búsqueda como Google suelen mostrar la meta descripción en los resultados de búsqueda, lo que puede influir en las tasas de clics:
  ! [Meta descripción] (_static/search-engine-optimization/meta-description.jpg)
  La meta descripción puede tener cualquier longitud, pero Google generalmente trunca los fragmentos a ~ 155-160 caracteres. Es mejor mantener las meta descripciones lo suficientemente largas como para que sean lo suficientemente descriptivas, por lo que se recomienda escribir descripciones entre 50 y 160 caracteres. Tenga en cuenta que la duración "óptima" variará según la situación, y su objetivo principal debe ser proporcionar valor y generar clics.
  

## Nombres de páginas compatibles con los motores de búsqueda

Para ver todos los nombres de páginas compatibles con los motores de búsqueda utilizados en la tienda, vaya a **Sistema → Nombres de páginas compatibles con los motores de búsqueda**.
![Nombres de páginas amigables para motores de búsqueda](_static/search-engine-optimization/seo-page-names-list.jpg)

Aquí puede filtrar los nombres de páginas compatibles con los motores de búsqueda por **Nombre**, **Idioma** o **Está activo** propiedad. También puede eliminar uno o varios nombres de páginas compatibles con los motores de búsqueda de filtros seleccionados utilizando el botón **Eliminar seleccionados**. En la columna **Editar página**, puede ver el botón que se utiliza para navegar a la página correspondiente.

## Ver también

* [Agregar productos](xref:en/running-your-store/catalog/products/add-products)
* [Categorías de productos](xref:en/running-your-store/catalog/categories)
* [Fabricantes](xref:en/running-your-store/catalog/Manufacturers)
* [Proveedores](xref:en/running-your-store / vendor-management)
* [Temas (páginas)](xref:en/running-your-store/content-management/topics-pages)
* [Noticias] (xref:en/running-your-store/content-management/news)
* [Blog] (xref:en/running-your-store/content-management/blog)

## Tutoriales

* [Comprensión de la configuración de SEO en nopCommerce](https://youtu.be/UxqM_nJyv1Q)
