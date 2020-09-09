---
title: Localization
uid: en/getting-started/advanced-configuration/localization
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.ivkadp, git.mariannk
---

# Localización

En nopCommerce, su tienda puede tener varios idiomas instalados. Sin embargo, los clientes solo verán los datos que se han definido en su idioma seleccionado.

> [!SUGERENCIA]
>
> De forma predeterminada, se instala el idioma inglés.

Para ver o editar los idiomas instalados, vaya a **Configuración → Idiomas**:
![idioma](_static/localization/Language.png)

> [!NOTA]
>
> Puede descargar nuevos paquetes de idiomas del [Marketplace] oficial (http://www.nopcommerce.com/marketplace).

## Añadiendo nuevo idioma

Para agregar un nuevo idioma, haga clic en **Agregar nuevo**. En la ventana *Agregar un nuevo idioma*, defina la siguiente configuración:
![addlanguage](_static/localization/addlanguage.png)

* El **Nombre** del nuevo idioma.
* La **Cultura del idioma**: un código de idioma específico (por ejemplo, de-AT para el alemán austriaco).
* El **Código SEO único**: un código SEO de dos letras que se utiliza para generar URL como `http: // www.yourstore.com / en /` cuando tienes más de un idioma publicado.

   > [!NOTA]
   >
   > La opción **URL amigables para SEO con varios idiomas** debe estar habilitada en el panel **Configuración → Configuración → Configuración general → Configuración de localización**.

* El **Nombre del archivo de imagen de la bandera**: ingrese el nombre del archivo de la imagen de la bandera. La imagen debe guardarse en el directorio `… / images / flags`. También puede elegir una imagen de una lista predefinida.
* Marque **De derecha a izquierda** si es necesario (por ejemplo, para árabe, hebreo, etc.).
  
  > [!NOTA]
  >
  > El tema activo debe ser compatible con RTL (tener un archivo de estilo CSS apropiado). Esta opción afecta solo a la tienda pública.

* La **moneda predeterminada** para un idioma específico. Si no se especifica, se utilizará el primero encontrado (con el orden de visualización más bajo).
* **Opción limitada a tiendas** que permite configurar este idioma para una tienda (s) específica (s). Puede elegir la (s) tienda (s) de una lista creada previamente. Deje este campo vacío si no usa esta opción.
  
  > [!NOTA]
  >
  > Para usar el límite de la tienda en la opción **Ignorar las reglas de "límite por tienda" (en todo el sitio)**, debe deshabilitarse en el panel **Configuración → Configuración → Configuración del catálogo → Rendimiento**.

* **Publica** el idioma, para permitir que este idioma sea visible y seleccionado por los visitantes de tu tienda.
* **Orden de visualización** del idioma. 1 representa la parte superior de la lista.

Haga clic en **Guardar** para guardar los cambios.

> [!NOTA]
>
> Después de agregar un nuevo idioma, podrá importar y exportar recursos de cadena utilizando **Importar recursos**
y botones **Exportar recursos** en la parte superior de la página. El panel *Recursos de cadenas* de la página de edición de idioma le permitirá ver los recursos de idioma existentes y agregar nuevos manualmente.

## Importar paquete de idioma

Si desea agregar un nuevo idioma a su tienda, debe:

1. Visite la página nopCommerce [traducciones] (https://www.nopcommerce.com/translations).
1. Elija la versión nopCommerce y descargue el paquete de idioma deseado.
1. Vaya a **Configuración → Idiomas** y presione el botón **Agregar nuevo**.
    ![LanguageAddNew](_static/localization /language-add-new.png)

1. Complete los campos obligatorios y haga clic en **Guardar y continuar con la edición**.
  ![LanguageSave] (_static/localization/language-save.png)

1. Haga clic en **Importar recursos**. Y especifique la ruta al archivo del paquete de idioma (*.xml) que descargó.
  ![LanguageImport] (_static /localization/language-import.png)

Si encontró un error en la traducción o desea tener un nombre personalizado, puede editar los recursos de cadena en el panel *Recursos de cadena*.

## Gestionar recursos de cadenas

Vaya a **Configuración → Idiomas**. Se muestra la ventana *Idiomas*:

![Idiomas](_static/localization/languages.png)

Haga clic en el botón **Editar** al lado del idioma. En la ventana **Editar detalles de idioma**, busque el panel **Recursos de cadenas**.

Por ejemplo, desea cambiar el nombre de un panel en la parte superior de la página de "Administración" (en la imagen de abajo) a "Panel de control".

![Ejemplo1](_static/localization/lang-example-before-change.jpeg)
 
1. En el campo Nombre del recurso, ingrese "administración". El recurso de cadena requerido si se encuentra. Haga clic en **Editar** junto a él.
1. Ingrese el nuevo nombre en el campo **Valor** y haga clic en **Actualizar**.
  ![Ejemplo2](_static/localization/lang-resource-edit.png)

1. Los cambios se implementan
  ![Ejemplo3](_static/localization/lang-example-after-change.jpeg)

Para agregar un nuevo recurso de cadena, use el panel ** Agregar nuevo registro **. Esta ventana le permite agregar un nuevo registro de recursos a la cuadrícula, de la siguiente manera:
![Agregar nuevo registro](_static/ localization/lang-add-resource.png)

* En el campo **Nombre del recurso**, ingrese el identificador de la cadena del recurso.
* En el campo **Valor**, ingrese un valor para este identificador de cadena de recursos.

Clic en **Guardar**.

## Configuración de localización

Para configurar los ajustes de localización, vaya a **Configuración → Ajustes → Ajustes generales**:

![Configuración de localización](_static/localization/lang-localization-settings.jpg)

- Para configurar el patrón [CLDR](http://cldr.unicode.org/) para la localización de la validación del lado del cliente de acuerdo con la cultura actual, haga clic en el botón **Establecer CLDR para la cultura actual**.
- Marque la casilla de verificación **Cargar todos los recursos locales al iniciar** para cargar todos los recursos locales al iniciar la aplicación. Cuando está habilitado, todos los recursos locales se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero todas las páginas podrían abrirse mucho más rápido.
- Marque la casilla de verificación **Cargar todas las propiedades localizadas al inicio** para cargar todas las propiedades localizadas al iniciar la aplicación. Cuando está habilitado, todas las propiedades localizadas (como las propiedades del producto localizadas) se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero todas las páginas podrían abrirse mucho más rápido. Se usa solo cuando tiene dos o más idiomas habilitados. No se recomienda habilitarlo cuando tiene un catálogo grande (varios miles de entidades localizadas).
- Marque la casilla de verificación **Cargar todos los nombres descriptivos del motor de búsqueda al inicio** para cargar todos los nombres descriptivos del motor de búsqueda al iniciar la aplicación. Cuando está habilitado, todos los slugs (nombres descriptivos de los motores de búsqueda) se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero todas las páginas podrían abrirse mucho más rápido. No se recomienda habilitarlo cuando tiene un catálogo grande.