---
title: Plugins in nopCommerce
uid: en/getting-started/advanced-configuration/plugins-in-nopcommerce
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Plugins en nopCommerce

Los plugins son un conjunto de componentes que agregan capacidades específicas a una tienda de nopCommerce. Ejemplos de plugins incluyen módulos de pago, métodos de cálculo de tasas de envío y más. En esta sección se describe cómo instalar plugins manualmente.

nopCommerce tiene una variedad de plugins, expandiendo sus funciones de tienda, en su [marketplace](http://www.nopcommerce.com/marketplace). Los plugins se pueden instalar ya sea descargando desde el mercado o accediendo al escaparate directamente desde el panel de administración.

Los plugins en el mercado se pueden ordenar por categoría, versión, nombre o calificación, y son gratuitos o de pago.

Los plugins disponibles en el mercado son desarrollados ya sea por el equipo de nopCommerce, socios de soluciones o proveedores externos.

> [!NOTA]
>
> Los plugins etiquetados "Por el equipo de nopCommerce" son desarrollados por el equipo de nopCommerce y se distribuyen libremente. Los conectores de servicios de terceros se desarrollan en el curso del programa de asociación *tecnología*,están sujetos a nopCommerce [servicios de soportepremium](http://www.nopcommerce.com/nopcommerce-premium-support-services) y también se distribuyenlibremente.

# Para instalar un plugin

1. El usuario tiene dos opciones para cargar el plugin. Puede utilizar cualquier que parezca más conveniente:
* Sube el plugin a la carpeta '/plugins'  en tu directorio de nopCommerce. Y reinicie su aplicación (o haga clic en el botón **Recargar lista de plugins**).  
* Sube el plugin o tema usando el botón **Subir plugin o tema**  indicando la ruta a la ubicación del archivo con el plugin en tu almacenamiento local.

> [!CONSEJO]
>
> Puede descargar más plugins de nopCommerce en nuestrodirectorio deextensiones[(https://www.nopcommerce.com/marketplacehttps://www.nopcommerce.com/marketplace).

![Subir plugin](_static/plugins-in-nopcommerce/plugin-upload.png)

1. Desplácese hacia abajo por la lista de plugins para encontrar el plugin recién instalado.
1. Haga clic en el enlace **Instalar**  para instalar el plugin.
1. Haga clic en el  botón Reiniciar aplicación para aplicar cambios en el panel superior para finalizar el proceso de instalación.
1. El plugin se muestra en la lista de plugins (**Configuration - Local plugins**).

> [!NOTA]
>
> Si está ejecutando nopCommerce en confianza media, entonces se recomienda borrar su directorio de ''Plugins''.  

# Para configurar un plugin

1. Ir a  **Configuración > Plugins locales**. Se muestra la lista de plugins:
![Plugins locales](_static/plugins-in-nopcommerce/local-plugins.png)
1. Haga clic en el enlace **Configurar**  junto al plugin para ir a la página de configuración del plugin. Si el botón **Configure**  no existe junto a un plugin, esto indica que el plugin no requiere ninguna configuración.

# Para cambiar el nombre descriptivo del plugin, muestre el orden y las limitaciones

1. Ir a  **Configuración > Plugins locales**. Se muestra la lista de plugins:
! [Plugins locales](_static/plugins-in-nopcommerce/local-plugins.png)
1. Haga clic en el botón Editar junto al plugin. Edite los detalles del plugin, de la siguiente manera:
! [Editar plugin](_static/plugins-in-nopcommerce/plugin-edit.jpg)
1. Introduzca el  **Nombre descriptivo**.
1. En el campo **Mostrar orden**, defina la ubicación necesaria para mostrar este plugin.
1. Marque el campo **Está habilitado**  si desea habilitar el plugin en la tienda.
1. En la lista desplegable **Limited to customer roles**  elija los roles que desea que pueda utilizar este plugin.
1. En el campo **Limitado a tiendas**,  defina las tiendas en las que se utilizará el plugin.
1. Haga clic en  **Guardar**  en la parte superior de la página.

# Para desinstalar un plugin

1. Ir a  **Configuración > Plugins locales**. Se muestra la lista de plugins:
![Plugins locales](_static/plugins-in-nopcommerce/local-plugins.png)
1. Haga clic en el enlace **Desinstalar junto al plugin para desinstalar. El plugin se desinstala. El enlace de la  columna De instalación  cambia a  **Instalar**  lo que le permite reinstalar el complemento en cualquier momento.
1. Haga clic en el  botón Reiniciar aplicación para aplicar cambios en el panel superior para finalizar el proceso de desinstalación.

# Tutoriales

- [Instalación de un plugin (para las versiones 3.90 - 4.10)](https://youtu.be/eLDsSm-4gKA)
- [Gestión del acceso a plugins por rol de cliente](https://www.youtube.com/watch?v=52lVVpQ3Qag)


