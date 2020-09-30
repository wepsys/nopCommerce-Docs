---
title: Your store information
uid: en/getting-started/advanced-configuration/your-store-information
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# La información de su tienda

De forma predeterminada, la instalación de nopCommerce, solo se crea una tienda y debe configurarse, como se describe a continuación.
Para configurar el almacén predeterminado, vaya a **Configuración > Tiendas**.

![mainstore](_static/your-store-information/mainstore.png)

Haga clic en Editar junto  a un almacén predeterminado para configurarlo.

![editstore](_static/your-store-information/Store-Edit.png)

Configure los detalles de la tienda principal, como se indica a continuación:

* Defina el  **Nombre de la tienda**.
* Introduzca la URL de la tienda de su tienda.
* Seleccione la casilla de verificación **SSL habilitado**  si su tienda está protegida por SSL. SSL (Secure Sockets Layer) es la tecnología de seguridad estándar para establecer un enlace cifrado entre un servidor web y un navegador. Este enlace garantiza que todos los datos pasados entre el servidor web y los navegadores permanezcan privados e integrales. SSL es un estándar de la industria y es utilizado por millones de sitios web en la protección de sus transacciones en línea con sus clientes.

> [!IMPORTANTE]
>
> Marque esta opción solo después de haber instalado el certificado SSL en el servidor. De lo contrario, no podrá acceder a su sitio y tendrá que editar manualmente el registro adecuado en la base de datos (tabla [Store]).

> [!CONSEJO]
>
> Obtenga más información sobre cómo configurar SSL en el siguiente capítulo: [Cómo instalar y configurar lacertificación SSL](xref:en/getting-started/advanced-configuration/how-to-install-and-configure-ssl-certification).

* El campo **VALORES HOST**  es una lista de posibles valores de HTTP_HOST de su tienda (por ejemplo,`yourstore.com`, `www.yourstore.com`). Rellenar este campo solo es necesario cuando tiene unasolución [multi-tienda](xref:en/getting-started/advanced-configuration/multi-store) para determinar el almacén actual. Este campo permite distinguir las solicitudes a direcciones URL distintas y determina el almacén actual. También puede ver el valor de HTTP_POST actual en  **Sistema > Información del sistema**.
* En el campo **Idioma predeterminado**,  elige un idioma predeterminado de tu tienda. También puede dejarlo sin seleccionar. En este caso, se utilizará el primero encontrado (con el orden de visualización más bajo).
* Definir el  **Orden de visualización**  para esta tienda.
* Definir el  **Nombre de la empresa**.
* Definir la **dirección de la empresa**.
* Establezca su  **Número de teléfono de la empresa**.
* En el campo **IVA de la empresa**, introduzca el IVA de su empresa (utilizada en la UE).

# Véase también

* [Configuración de multi-Store](xref:en/getting-started/advanced-configuration/multi-store)
* [Países](xref:en/getting-started/configure-shipping/advanced-configuration/countries-states)
* [Idiomas](xref:en/getting-started/advanced-configuration/localization)
* [Ajustes de seguridad](xref:en/getting-started/advanced-configuration/security-settings)
* [Ajustes PDF](xref:en/getting-started/advanced-configuration/pdf-settings)
* [Ajustes del RGPD](xref:en/getting-started/advanced-configuration/gdpr-settings)


