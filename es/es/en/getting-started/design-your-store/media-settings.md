---
title: Media settings
uid: en/getting-started/design-your-store/media-settings
author: git.AndreiMaz
contributors: git.exileDev, git.DmitriyKulagin, git.mariannk
---

# Ajustes de los medios de comunicación

Esta sección describe cómo configurar los detalles de los medios de comunicación de su tienda. Esto incluye la definición del producto, las variantes y el tamaño de las imágenes de los avatares y más.

Para definir los ajustes de los medios de comunicación vaya a **Configuración → Ajustes → Ajustes de los medios de comunicación**. Aparecerá la ventana *Configuración de los medios*:

![p1](_static/media-settings/media_sett_1.png)

En el panel *Común* defina los ajustes, de la siguiente manera:
- Haga clic en el botón **Cambiar** de arriba **Las imágenes se almacenan en** para elegir entre la base de datos o el sistema de archivos.

  > [!NOTE]
  > 
  > Se recomienda hacer una copia de seguridad de la base de datos antes de pulsar el botón **Cambiar**.
- En el campo **Tamaño máximo de la imagen**, introduzca el tamaño máximo de la imagen (es decir, el lado más largo) permitido para la carga de la imagen (en píxeles).
- Marque **Directorios de pulgares múltiples** para tener varios directorios de pulgares. Es útil cuando su empresa de alojamiento tiene limitaciones en la cantidad de archivos por directorio.
- En la casilla **Calidad de imagen por defecto (0 - 100)** introduzca la calidad de las imágenes subidas. Una vez cambiado, tienes que borrar manualmente todos los pulgares ya generados.
- Marque **Importar imágenes de productos usando hash** para usar HASHBYTES para comparar las imágenes con los productos cargados. Tenga en cuenta que esta funcionalidad no está soportada por algunas bases de datos.
- Marque **Zoom de imagen** para habilitar el zoom de la imagen en la página de detalles del producto.

En el panel *Producto* defina los ajustes, como sigue:
- En el campo **Tamaño de la imagen de detalle del producto**, introduzca el tamaño predeterminado para las imágenes de detalle del producto en píxeles.
- En el campo **Tamaño de la imagen en miniatura del producto (catálogo)**, introduzca el tamaño predeterminado para las imágenes en miniatura del producto que se muestran en las páginas de la categoría o del fabricante en píxeles.
- En el campo **Tamaño de la imagen en miniatura del producto (página del producto)**, introduce el tamaño predeterminado de las imágenes en miniatura del producto (en píxeles) que se muestran en la página de detalles del producto (utilizado cuando tienes más de una imagen del producto).
- En el campo **Tamaño de la imagen del producto asociado**, introduzca el tamaño predeterminado para las imágenes del producto asociado en píxeles. Los productos asociados forman parte de los productos agrupados.

En el panel *Otras páginas* defina los ajustes, de la siguiente manera:
- En el campo **Tamaño de la imagen en miniatura de la categoría**, introduzca el tamaño predeterminado para las imágenes en miniatura del producto en las páginas de la categoría en píxeles.
- En el campo **Tamaño de la imagen en miniatura del fabricante**, introduzca el tamaño predeterminado para las imágenes en miniatura del producto en las páginas del fabricante en píxeles.
- En el campo **Tamaño de la imagen en miniatura del proveedor**, introduzca el tamaño predeterminado para las imágenes en miniatura del producto en las páginas del proveedor en píxeles.
- En el campo **Tamaño de la imagen en miniatura del carro/ lista de deseos**, introduzca el tamaño por defecto de las imágenes en miniatura del producto en el carro de la compra y la lista de deseos en píxeles.
- En el campo **Tamaño de la imagen en miniatura del carro de la compra**, introduzca el tamaño por defecto (en píxeles) de las imágenes en miniatura del producto que se muestran en el bloque del carro de la compra.
- En el campo **Tamaño de la imagen del avatar**, introduce el tamaño por defecto de las imágenes del avatar.

Esta página habilita **configuración multitienda**, significa que se pueden definir las mismas configuraciones para todas las tiendas o que pueden ser diferentes de una tienda a otra. Si quieres gestionar la configuración de una tienda determinada, elige su nombre de la lista *configuración de varias tiendas* y marca todas las casillas de verificación necesarias en el lado izquierdo para establecer un valor personalizado para ellas.

## Tutoriales

- [Managing media settings](https://www.youtube.com/watch?v=3JS4Zj4TBwQ)
