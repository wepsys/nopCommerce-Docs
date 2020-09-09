---
title: Multi-store
uid: en/getting-started/advanced-configuration/multi-store
author: git.AndreiMaz
contributors: git.rajupaladiya, git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Multi-tienda

nopCommerce le permite ejecutar más de una tienda utilizando una interfaz desde una sola instalación de nopCommerce.

Esto le permite hospedar más de un almacén front-end en diferentes dominios y administrar todas las operaciones de administración desde el panel de administración único. Puede compartir los datos del catálogo entre tiendas, tener un producto en más de una tienda, por ejemplo, y sus clientes pueden iniciar sesión en todas sus tiendas con las mismas credenciales.

# Configuración de varias tiendas

### 1. Parte del panel de control de alojamiento

En el siguiente ejemplo describiremos la configuración de dos almacenes de ejemplo, como se indica a continuación:

* `www.store1.com`
* `www.store2.com`

1. Cargue e instale el sitio en  'www.store1.com'. Este es el único lugar donde se almacenan los archivos nopCommerce y DLL.
> [!NOTA]
>
> Leer más cómo instalar nopCommerce en el siguiente capítulo: [Instalación denopCommerce](xref:en/installation-and-upgrading/installing-nopcommerce/index).

1. Desde el panel de control de  `www.store2.com`  (es decir, su panel de control de hosting, no el área de administración de nopCommerce) asegúrese de que todas las solicitudes a  'www.store2.com' se reenvíen (no se redirigen) a  'www.store1.com'. Realice esto mediante registros CNAME. Este paso es crucial.

1. En el panel de control de  `www.store1.com`,configure un alias de dominio para  `www.store2.com`. Este paso puede ser complicado para algunos usuarios (pídale al administrador del sistema que realice este paso si tiene problemas).

Después de completar los pasos anteriores, al acceder a 'www.store2.com'  desde su navegador, se mostrará el contenido de 'www.store1.com'.  El siguiente paso es configurar las tiendas en el área de administración de nopCommerce que se describirá a continuación. A continuación, puede empezar a cargar contenido para ambas tiendas.

1. Opcional (muestra): Este paso se puede realizar desde el panel de control de Plesk a continuación, de la siguiente manera:
  
Cuando 'www.store2.com'  se redirige a  'www.store1.com', el servidor web dePlesk no sabe cómo mostrar  'www.store2.com'  ya que utiliza el hosting virtual basado en nombres. Por lo tanto, debe crear un alias de dominio para  'www.store2.com',como se describe a continuación:

* Inicie sesión en el panel de dominio de  'www.store1.com',ya sea directamente o a través del enlace **Abrir en el Panel de control**  desde el panel de administración del servidor.

* En la pestaña **Sitios web y dominios**,  seleccione el enlace **Agregar nuevo alias de dominio**  cerca de la parte inferior de la pestaña.

* Introduzca el alias completo. Por ejemplo -  'store2.com'.

* Asegúrese de que la opción **Servicio web**  esté seleccionada.

* El servicio **Mail**  es opcional. Marque esta opción si desea que los correos electrónicos de  'www.store2.com'  se redirijan de una manera similar.

* Asegúrese de que la opción **Sincronizar zona DNS con el dominio principal**  está desactivada.

### 2. parte del área de administración de nopCommerce

Una vez finalizada la instalación y la configuración técnica, puedes gestionar tus tiendas desde el área de administración de nopCommerce. Ir a **Configuración > Tiendas**. Aparece la ventana *Tiendas*:  

![Ventana Tiendas](_static/multi-store/mainstore.png)

> [!NOTA]
>
> De forma predeterminada, solo se crea una tienda.

Para configurar varias tiendas, haga clic en **Agregar nuevo**  y defina la siguiente configuración de tienda:

![Crear](_static/multi-store/create.jpg)

* Defina el  **Nombre de la tienda**.
* Introduzca la URL de la tienda de su tienda.
* Seleccione la casilla de verificación **SSL habilitado**  si su tienda está protegida por SSL. SSL (Secure Sockets Layer) es la tecnología de seguridad estándar para establecer un enlace cifrado entre un servidor web y un navegador. Este enlace garantiza que todos los datos pasados entre el servidor web y los navegadores permanezcan privados e integrales. SSL es un estándar de la industria y es utilizado por millones de sitios web en la protección de sus transacciones en línea con sus clientes.

> [!IMPORTANTE]
>
> Marque esta opción solo después de haber instalado el certificado SSL en el servidor. De lo contrario, no podrá acceder a su sitio y tendrá que editar manualmente el registro adecuado en la base de datos (tabla [Store]).

> [!CONSEJO]
>
> Obtenga más información sobre cómo configurar SSL en el siguiente capítulo: [Cómo instalar y configurar lacertificación SSL](xref:en/getting-started/advanced-configuration/how-to-install-and-configure-ssl-certification).

* El campo **VALORES HOST**  es una lista de posibles valores de HTTP_HOST de su tienda (por ejemplo,  'store1.com',  'www.store1.com'). Rellenar este campo solo es necesario cuando tiene una solución de varias tiendas para determinar el almacén actual. Este campo permite distinguir las solicitudes a direcciones URL distintas y determina el almacén actual. También puede ver el valor de HTTP_POST actual en  **Sistema > Información del sistema**.
* En el campo **Idioma predeterminado**,  elige un idioma predeterminado de tu tienda. También puede dejarlo sin seleccionar. En este caso, se utilizará el primero encontrado (con el orden de visualización más bajo).
* Definir el  **Orden de visualización**  para esta tienda.
* Definir el  **Nombre de la empresa**.
* Definir la dirección de la empresa ***.
* Establezca su  **Número de teléfono de la empresa**.
* En el campo **IVA de la empresa**, introduzca el IVA de su empresa (utilizada en la UE).

Agregue otra tienda haciendo clic en el botón  **Agregar nuevo** en la página **Configuración > Almacenes**  y rellenando los campos similares.

Las dos tiendas se han configurado utilizando una sola instalación de nopCommerce, de la siguiente manera:

* www.store1.com
* www.store2.com

> [!NOTA]
>
> La solución multise tienda (distinción de almacenes por HTTP_HOST) no funciona para sitios en directorios virtuales en el mismo dominio.

Por ejemplo, no puede tener una tienda en `http://www.site.com/store1`  y la segunda tienda en  `http://www.site.com/store2`,ya que el valor HTTP_HOST para ambos sitios es el mismo ('www.site.com').).

# Configuración de entidades para varias tiendas

Una vez que las tiendas se han configurado y configurado, puede definir las entidades para cada tienda. Para ello, rellene el campo **Limited to stores**  de las páginas de detalles para cada una de las siguientes páginas: [Products](xref:en/running-your-store/catalog/products/index),[Categories](xref:en/running-su tienda/catálogo/categorías),[Fabricantes](xref:en/running-your-store/catalog/manufacturers),[Idiomas](xref:en/getting-started/advanced-configuration/localization),[Currencies](xref:en/getting-started/configure-payments/advanced-configuration/currencies),[Plantillas demensajes](xref:en/running-your-store/content-management/message-templates),[Blogs](xref:en/running-running-templates su-store/content-management/blog),[Noticias](xref:en/running-your-store/content-management/news),[Topics](xref:en/running-your-store/content-management/topics-pages).

Desplácese hacia abajo hasta el campo **Limitado a tiendas**  y elija el nombre de la tienda existente en el menú desplegable, como se muestra en la pantalla *Editar detalles del producto*  a continuación:

![Asignaciones](_static/multi-store/product-limited-to-store.png)

# Configuración de los ajustes para varias tiendas

Diferentes [temas](xref:en/getting-started/design-your-store/choose-and-install-a-theme) también se pueden configurar para diferentestiendas.

Además, puede invalidar cualquier valor de configuración por tienda. Por ejemplo, vaya a **Configuración > Configuración de pedido**  y vea el menú desplegable Configuración de varias tiendas para**  donde puede elegir la tienda para la que desea invalidar la configuración:

![Ajustes de invalidación](_static/multi-store/override-settings.jpg)

Cuando elija la tienda, la página se actualizará y podrá definir cualquier campo para la tienda elegida. A continuación, haga clic en **Guardar**  para guardar la configuración.

