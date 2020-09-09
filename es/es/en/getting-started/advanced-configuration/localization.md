---
title: Localization
uid: en/getting-started/advanced-configuration/localization
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.ivkadp, git.mariannk
---

# Localization

En nopCommerce, tu tienda puede tener varios idiomas instalados. Sin embargo, los clientes solo verán los datos que se han definido en su idioma seleccionado.

> [!CONSEJO]
>
> De forma predeterminada, el idioma inglés está instalado.

Para ver o editar los idiomas instalados, vaya a **Configuración > Idiomas**:
![idioma](_static/localization/Language.png)

> [!NOTA]
>
> Puede descargar nuevos paquetes de idioma desde el oficial [Marketplace](http://www.nopcommerce.com/marketplace).

# Adición de nuevo idioma

Para agregar un nuevo idioma, haga clic en **Agregar nuevo**. En la ventana *Agregar un nuevo idioma*,  defina los siguientes ajustes:

![addlanguage](_static/localization/addlanguage.png)

* El  **Nombre**  del nuevo idioma.
* La  cultura del **idioma** - un código de idioma específico (por ejemplo, de-AT para el alemán austriaco).
* El  **código SEO único**  - un código SEO de dos letras utilizado para generar URLs como   `http://www.yourstore.com/en/`  cuando tienes más de un idioma publicado.

> [!NOTA]
>
> La opción URL amigables con SEO con varios idiomas**  debe estar habilitada en el panel **Configuración > Configuración > Ajustes generales > Configuración de localización**.  

* El  **Flag nombre de archivo de imagen**  - introduzca el nombre del archivo de imagen de la bandera. La imagen debe guardarse en el directorio `.../images/flags`.  También puede elegir una imagen de una lista predefinida.
* Marque  **de derecha a izquierda**  si es necesario (por ejemplo, para árabe, hebreo, etc.).
  
> [!NOTA]
>
> El tema activo debe ser compatible con RTL (tiene un archivo de estilo CSS adecuado). Esta opción solo afecta al almacén público.

* La  moneda predeterminada para un idioma específico. Si no se especifica, se utilizará el primero encontrado (con el orden de visualización más bajo).
* **Limitado a la opción de tiendas**  lo que permite establecer este idioma para una(s) tienda(s) específica(s). Puede elegir las tiendas de una lista creada previamente. Deje este campo vacío si no utiliza esta opción.
  
> [!NOTA]
>
> Para utilizar el limitton de la tienda, la opción **Ignorar reglas de "límite por tienda" (en todo el sitio)**  debe estar desactivada en el panel **Configuración > Configuración > Configuración del catálogo > Rendimiento**.  

* **Publicar**  el idioma, para permitir que este idioma sea visible y seleccionado por los visitantes de su tienda.
* **Mostrar orden**  del idioma. 1 representa la parte superior de la lista.

Haga clic en Guardar para  guardar los cambios.

> [!NOTA]
>
> Después de agregar un nuevo idioma, podrá importar y exportar recursos de cadena utilizando los recursos de importación**
y los botones Exportar recursos**  en la parte superior de la página. El panel *Recursos de cadena*  de la página de edición de idioma le permitirá ver los recursos de idioma existentes y agregar otros nuevos manualmente.

# Paquete de idioma de importación

Si desea agregar un nuevo idioma a su tienda, debe:

1. Visita la página nopCommerce [traducciones](https://www.nopcommerce.com/translations).
1. Elija la versión nopCommerce y descargue el paquete de idioma deseado.
1. Ir a  **Configuración > Idiomas**  y pulse el botón AddNew.*.  
![LanguageAddNew](_static/localization/language-add-new.png)

1. Rellene los campos obligatorios y haga clic en  **Guardar y continuar editando**.
![LanguageSave](_static/localization/language-save.png)

1. Haga clic en  **Importar recursos**. Y especifique la ruta de acceso al archivo de paquete de idioma (*.xml) que descargó.
![LanguageImport](_static/localization/language-import.png)

Si ha encontrado un error en la traducción o desea tener nombres personalizados, puede editar los recursos de cadena en el panel *Recursos de  cadena*.

# Administrar recursos de cadena

Ir a **Configuración > Idiomas**. Aparece la ventana *Idiomas*:  

![Idiomas](_static/localization/languages.png)

Haga clic en el botón Editar junto  al idioma. En la ventana Detalles del idioma de  edición, busque el panel **Recursos de cadena**.  

Por ejemplo, desea cambiar el nombre de un panel en la parte superior de la página de "Administración" (en la imagen de abajo) a "Panel de control".

![Ejemplo 1](_static/localization/lang-example-before-change.jpeg)
 
1. En el campo Nombre de recurso, escriba "administración". El recurso de cadena necesario si se encuentra. Haga clic en  Editar junto a él.
1. Introduzca el nuevo nombre en el campo **Valor**  y haga clic en  **Actualizar**.
![Ejemplo 2](_static/localization/lang-resource-edit.png)

1. Los cambios se implementan
![Ejemplo 3](_static/localization/lang-example-after-change.jpeg)

Para agregar un nuevo recurso de cadena, utilice el panel **Agregar nuevo registro**.  Esta ventana le permite agregar un nuevo registro de recursos a la cuadrícula, como se indica a continuación:
![Agregar nuevo registro](_static/localization/lang-add-resource.png)

* En el campo **Nombre de recurso**, escriba el identificador de cadena de recursos.
* En el campo **Value**,  escriba un valor para este identificador de cadena de recursos.

Haga clic en **Guardar**.

# Configuración de localización

Para configurar los ajustes de localización, vaya a **Configuración > Configuración > Ajustes generales**:

![Ajustes de localización](_static/localización/lang-localization-settings.jpg)

- Para establecer elpatrón [CLDR](http://cldr.unicode.org/) parala localización de la validación del lado cliente de acuerdo con la referencia cultural actual, haga clic en el botón **Set CLDR for current culture**.  
- Marque la casilla de verificación  **Cargar todos los recursos de configuración regional al iniciar**  para cargar todos los recursos locales al iniciar la aplicación. Cuando está habilitado, todos los recursos de configuración regional se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero entonces todas las páginas podrían abrirse mucho más rápido.
- Marque la casilla de verificación  **Cargar todas las propiedades localizadas al inicio**  para cargar todas las propiedades localizadas al iniciar la aplicación. Cuando está habilitada, todas las propiedades localizadas (como las propiedades localizadas del producto) se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero entonces todas las páginas podrían abrirse mucho más rápido. Solo se usa cuando tiene dos o más idiomas habilitados. No se recomienda habilitar cuando tiene un catálogo grande (varios miles de entidades localizadas).
- Marque la casilla de verificación  **Cargar todos los nombres descriptivos del motor de búsqueda en el inicio**  para cargar todos los nombres descriptivos del motor de búsqueda en el inicio de la aplicación. Cuando está habilitado, todos los slugs (nombres descriptivos del motor de búsqueda) se cargarán al iniciar la aplicación. El inicio de la aplicación será más lento, pero entonces todas las páginas podrían abrirse mucho más rápido. No se recomienda habilitar cuando tiene un catálogo grande (varios miles de entidades).
- Marque la casilla de verificación  **Usar imágenes para la selección de idioma**  para utilizar imágenes en lugar de nombres de idioma.
- Marque la casilla de verificación  **URLs amigables SEO con varios idiomas habilitados**  para permitir URLs amigables con SEO para todos los idiomas. Cuando está habilitada, sus URL serán  `http://www.yourStore.com/en/`  o  `http://www.yourStore.com/ru/`  (se admiten SEO).
- Marque la casilla de verificación  **Detectar automáticamente el idioma**  para detectar el idioma en función de la configuración del navegador del cliente.

# Localizar entidades

Si tiene más de un idioma instalado en su tienda, podrá introducir algunos campos que se muestran a los clientes en diferentes idiomas. Por ejemplo:

![Campos](_static/localization/fields.jpg)

- En la ficha *Estándar* introduzca el texto que se mostrará a los clientes si no se especifican los campos localizados.
- En las  *pestañas con nombres de idioma*  introduzca el texto localizado.

