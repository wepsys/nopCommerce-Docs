---
title: Customizing nopCommerce Themes
uid: es/developer/design/customizing-theme
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Personalización de temas de nopCommerce

## Subiendo el logotipo de su tienda
Para cargar el logotipo de su tienda en un sitio web de nopCommerce, existen básicamente 2 métodos:s:

### Primer método

1. Ir a la carpeta raíz de nopCommerce `/Themes/YOUR THEME/Content/images/`
1. Busque el archivo de imagen logo.gif
1.Reemplace el `logo.gif` con el logotipo de su tienda y asígnele el nombre `logo.gif` (con el mismo ancho: 310px y alto: 60px)

### Segundo método

1. Guarde el logotipo de su tienda en esta ubicación: carpeta raíz nopCommerce `/Themes/YOUR THEME/Content/images/`
1. Ir a la carpeta raíz de nopCommerce `/Views/Shared/Header.cshtml`
1. Abra el archivo `Header.cshtml`
1. Busque este código en la parte superior:

    ```csharp
    var logoPath = "~/Themes/" + currentThemeName + "/Content/images/logo.gif";
    ```

    Puede mencionar la ruta de su logotipo personalizado aquí.

    > [!NOTE]
    > 
    > En el código css mencionado anteriormente: logo.gif es el nombre del archivo de imagen del logotipo de la tienda

1. Cambiar logo.gif con `YourLogo.gif/jpg/png`
1. Guarde los cambios en el `Header.cshtml` file
> 

> [!IMPORTANT]
>
>Es posible que deba actualizar el navegador o eliminar el historial o las cookies de su navegador para ver los cambios (nuevo logotipo de la tienda).

Si desea realizar cambios en la hoja de estilo con respecto al logotipo, busque el siguiente código en su `styles.css`:

```css
.header-logo {
    margin: 0 0 20px;
    text-align: center;
}
.header-logo a {
    display: inline-block;
    max-width: 100%;
    line-height: 0; /*firefox line-height bug fix*/
}
.header-logo a img {
    max-width: 100%;
    opacity: 1;
}
```

## Cómo cambiar un diseño

1. /  si deceas realizar cambios en el diseño base (i.e. `_Root.cshtml`) de su sitio web nopCommerce. Busque este código CSS en su `style.css`

    ```css
    .master-wrapper-content {
        position: relative;
        z-index: 0;
        width: 90%;
        margin: 0 auto;
    }
    .master-column-wrapper {
        position: relative;
        z-index: 0;
    }
    .master-column-wrapper:after {
        content: "";
        display: block;
        clear: both;
    }
    ```

1. Si desea personalizar/realizar cambios en el diseño de `_ColumnOne.cshtml`. Busque este código CSS en su `style.css`

    ```css
    .center-1 {
        margin: 0 0 100px;
    }
    ```

1. Si desea personalizar/realizar cambios en el diseño de `_ColumnTwo.cshtml`.  `style.css`

    ```css
        .center-2, .side-2 {
        margin: 0 0 50px;
    }
    .side-2:after {
        content: "";
        display: block;
        clear: both;
    }
    ```

## Cómo realizar cambios en el menú de encabezado (menú superior)

1. Si desea personalizar/realizar cambios en el menú de encabezado (menú superior) de su sitio web nopCommerce, vaya a la siguiente ubicación:

    Ir a la carpeta raíz de nopCommerce `/Views/Shared/Components/TopMenu/Default.cshtml`
1. Abrir archivo `Default.cshtml` - Puede agregar o eliminar elementos de menú en` <li> `según sus requisitos.

## Cómo realizar cambios en el pie de página (o enlaces de pie de página)

1. Si desea personalizar/realizar cambios en un pie de página (o enlaces de pie de página) de su sitio web nopCommerce, vaya a la siguiente ubicación:

    Ir a la carpeta raíz de nopCommerce `/Views/Shared/Components/Footer/Default.cshtml`
1. Abra el archivo `Default.cshtml` - Puede agregar o eliminar enlaces en` <li> `o completar` <ul> `según sus requisitos.