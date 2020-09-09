---
title: Understanding Layout / Design
uid: en/developer/design/understanding-layout
author: git.AndreiMaz
contributors: git.exileDev, git.DmitriyKulagin
---

# Comprensión del diseño / Diseño

¿Qué son los diseños? Cada desarrollador/diseñador web quiere mantener un aspecto y una sensación coherentes en todas las páginas del sitio web. En los días, el concepto de "páginas maestras" se introdujo en ASP.NET 2.0 que ayuda a mantener un aspecto coherente del sitio web mediante la asignación con páginas .aspx.

Razor también soporta este concepto similar con una característica llamada "Layouts". Básicamente, le permite definir una plantilla de sitio común y luego heredar su aspecto a través de todas las vistas / páginas de su sitio web.

En nopCommerce, hay 2 tipos diferentes de diseños:

* '_ColumnsOne.cshtml'
* '_ColumnsTwo.cshtml'

Todos estos 2 diseños se heredan de un diseño principal llamado: '_Root.cshtml'. El  '_Root.cshtml'  se hereda de  '_Root.Head.cshtml'. '_Root.Head.cshtml'  es el archivo que debe examinar si está vinculado a archivos css stylesheet y jquery (puede agregar/vincular más archivos '.css'  y  '.js'  aquí). La ubicación de todos estos diseños en nopCommerce es la siguiente:  '[directorio raíz de nopCommerce]/Views/Shared/...'. Si está utilizando la versión de código fuente, entonces:  ''Presentación'Nop.Web'Vistas'''

* **Diseño de _Root.cshtml**

![root-layout](_static/understanding-layout/root-layout.jpg)

* **Diseño de  '_Root.cshtml'  (con respecto a la clase css)**

![root-layout-css](_static/understanding-layout/root-layout-css.jpg)

Ahora los siguientes 2 diseños anulan el cuerpo de '_Root.cshtml':

* '_ColumnsOne.cshtml'

En este caso, no hay ningún cambio en el diseño del cuerpo, por lo que la estructura sigue siendo prácticamente la misma que '_Root.cshtml':

![columnas-uno](_static/understanding-layout/column-one.jpg)

* '_ColumnsTwo.cshtml'

En este caso, hay 2 columnas en la estructura del cuerpo:

![columna-dos](_static/understanding-layout/column-two.jpg)


