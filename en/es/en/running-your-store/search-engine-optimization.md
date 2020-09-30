---
title: Search engine optimization
uid: en/running-your-store/search-engine-optimization
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Optimización del motor de búsqueda

SEO significa optimización de motores de búsqueda, es un proceso de obtener tráfico de resultados de búsqueda "gratuitos", "orgánicos", "editoriales" o "naturales" en los motores de búsqueda. Todos los principales motores de búsqueda tienen resultados de búsqueda primarios, en los que se muestran y clasifican las páginas web y otros contenidos, como vídeos o listados locales, en función de lo que un motor de búsqueda considera más relevante para los usuarios.

nopCommerce apoya las técnicas de SEO para los diferentes tipos de páginas de su tienda. Encuentra una lista de ellas en la sección [See also](#see-also)

## Ajustes de SEO

Hay algunos ajustes generales de SEO en nopCommerce, que se pueden aplicar a toda la tienda.

Para editar la configuración de SEO, vaya a **Configuración → Configuración → Configuración general**.

![SEO settings](_static/search-engine-optimization/seo1.png)

* In the **Default title** field, enter the default title of your store pages.
* In the field **Page title SEO setting**, select the required page title SEO setting as follows:

  * El nombre de la página viene después del nombre de la tienda en el título:
  `YOURSTORE.COM` | PAGENAME

  * El nombre de la tienda viene después del nombre de la página en el título:
  PAGENAME | `YOURSTORE.COM`

* Especifique el **Separador de título de la página**.
* Introduce las **Palabras clave meta predeterminadas** para las páginas de tu tienda. Esto puede ser anulado para categorías individuales, fabricantes, productos y algunas otras páginas.
* Introduzca la **Descripción meta predeterminada** para las páginas de su tienda. Esto puede ser anulado para categorías individuales, fabricantes, productos y algunas otras páginas.
* Seleccione la **Generación de la descripción META del producto**, para generar automáticamente las descripciones META del producto (si no se especifica en la página de detalles del producto) basadas en la descripción corta del producto.
* Seleccione el **Requisito del prefijo WWW**. Por ejemplo, `http://yourStore.com/` podría ser redirigido automáticamente a `http://www.yourStore.com/`. Seleccione una de las siguientes opciones:
    * *No importa*
    * * Las páginas deben tener el prefijo WWW *
    * Las páginas no deben tener el prefijo WWW *
* Selecciona la casilla **Convertir caracteres no occidentales**, para eliminar el acento en los nombres de SEO. Por ejemplo, convertir é a e.
* Seleccione la casilla de verificación **Habilitar URLs canónicos**, para transformar un URL en un URL canónico y así poder determinar si dos URLs sintácticamente diferentes pueden llevar a una página con el contenido equivalente.
* Marque la casilla de verificación **Twitter META tags** para generar etiquetas META de Twitter en la página de detalles del producto.
* Marque la casilla de verificación **Open Graph META tags** para generar etiquetas META Open Graph en la página de detalles del producto.
* Marque la casilla de verificación **Microdata tags** para generar etiquetas de Microdatos en la página de detalles del producto.
* Introduce la etiqueta **Custom &#60;head&#62; tag**. Por ejemplo, algunas etiquetas personalizadas de &#60;meta&#62;. O déjela vacía si ignora esta configuración.

## Paneles de SEO

Hay varios tipos de páginas en nopCommerce para las que se pueden configurar ajustes individuales de SEO, incluyendo meta palabras clave, meta descripción, meta título y nombres de páginas amigables para los motores de búsqueda. Esto se hace en los paneles de SEO de las correspondientes secciones del área de administración.

![SEO panel](_static/search-engine-optimization/seo-panel.jpg)

* En el campo **Nombre de la página compatible con los motores de búsqueda**, introduzca el nombre de la página utilizada por los motores de búsqueda. Si no introduce nada, la URL de la página web se forma utilizando el nombre de la página. Si introduces *nombre de página personalizado*, entonces se utilizará el siguiente URL personalizado: `http://www.yourStore.com/custom-seo-page-name`.

* En el campo **Título de Meta**, introduzca el título requerido. La etiqueta del título especifica el título de su página web. Es recuperada por los navegadores web y también es utilizada por los motores de búsqueda como Google para mostrar una página web en los resultados de búsqueda:
  ![Meta title](_static/search-engine-optimization/meta-title.jpg)

* Introduce las **Meta palabras clave** requeridas. Describen el contenido de una página web de forma breve y concisa y por lo tanto son importantes indicadores del contenido de un sitio web para los motores de búsqueda. Las meta palabras clave ayudan a decirle a los motores de búsqueda cuál es el tema de la página. Las palabras clave se escriben generalmente en minúsculas.

* En el campo **Descripción de las meta palabras**, introduzca una descripción de la página. La meta descripción proporciona un resumen de una página web. Los motores de búsqueda como Google a menudo muestran la meta descripción en los resultados de búsqueda, lo que puede influir en los índices de clics:
  ![Meta descripción](_static/search-engine-optimization/meta-description.jpg)
  La meta descripción puede ser de cualquier longitud, pero Google generalmente trunca los fragmentos a ~155-160 caracteres. Es mejor mantener las meta descripciones lo suficientemente largas para que sean lo suficientemente descriptivas, por lo que se recomienda escribir descripciones entre 50-160 caracteres. Ten en cuenta que la longitud "óptima" variará en función de la situación, y tu objetivo principal debe ser proporcionar valor y generar clics.
  

## Nombres de páginas aptas para los motores de búsqueda

Para ver todos los nombres de páginas amigables para los motores de búsqueda usados en la tienda, ve a **Sistema → Nombres de páginas amigables para los motores de búsqueda**.
![Search engine friendly page names](_static/search-engine-optimization/seo-page-names-list.jpg)

Aquí puedes filtrar los nombres de las páginas amigas de los buscadores por **Nombre**, **Idioma** o **Es activo** propiedad. También puede eliminar uno o varios de los nombres de las páginas amigables para los motores de búsqueda seleccionados utilizando el botón **Borrar seleccionados**. En la columna **Editar página** puede ver el botón utilizado para navegar a la página apropiada.

## See also

* [Adding products](xref:en/running-your-store/catalog/products/add-products)
* [Product categories](xref:en/running-your-store/catalog/categories)
* [Manufacturers](xref:en/running-your-store/catalog/manufacturers)
* [Vendors](xref:en/running-your-store/vendor-management)
* [Topics (pages)](xref:en/running-your-store/content-management/topics-pages)
* [News](xref:en/running-your-store/content-management/news)
* [Blog](xref:en/running-your-store/content-management/blog)

## Tutoriales

* [Understanding SEO settings in nopCommerce](https://youtu.be/UxqM_nJyv1Q)
