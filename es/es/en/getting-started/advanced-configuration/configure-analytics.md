---
title: Configure analytics
uid: en/getting-started/advanced-configuration/configure-analytics
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Complemento de análisis de Google

En esta sección se describe cómo agregar e integrar el complemento **Google Analytics**  en tu tienda.

Para configurar el complemento de análisis de Google:

Ir a **Configuración > Widgets**. Se muestra la ventana *Widgets*:  

![Widgets](_static/configure-analytics/google-analytics-widgets.png)

# Activar el plugin

Haga clic en Editar junto a la análisis  de Google. La ventana se expande, como se indica a continuación:

![Análisis de Google](_static/configure-analytics/google-analytics-widgets-edit.jpg)

Seleccione la casilla de verificación **Está activo**  para habilitar el complemento de análisis de Google. Haga clic en el botón Actualizar para guardar los cambios.

# Configurar el plugin

Haga clic en **Configurar**  junto a la  análisis de Google. Se muestra la ventana *Configurar – Análisis de Google*,  como se indica a continuación:

![Análisis de Google - Configurar](_static/configure-analytics/google-analytics-widgets-configure.png)

Realice los pasos siguientes para habilitar la integración de Google Analytics:

* Crear una cuenta de análisis de Google **  en el siguiente enlace [http://www.google.com/analytics/](http://www.google.com/analytics/) y siga el asistente para agregar su sitioweb
* Copie el ID de análisis de Google en  el cuadro **ID**  del formulario.
* Introduzca el  **Código de seguimiento**  generado por Google Analytics. Se reemplazarán dinámicamente los archivos GOOGLEID y CUSTOMER_TRACKING.
* Marque la casilla de verificación **Habilitar comercio electrónico** para pasar información sobre pedidos a la función de comercio electrónico de Google. Si marca los campos de folloeing se mostrarán:
* Marque  **Use JS para enviar información de comercio electrónico**  para usar el código JS para enviar información de comercio electrónico desde la página de pedido completada. Pero en caso de métodos de pago de redirección algunos clientes pueden omitirlo. De lo contrario, la información de comercio electrónico se enviará mediante la solicitud HTTP. La información se envía cada vez que se paga un pedido, pero UTM no se admite en este modo. 
* Marque  **Incluir impuestos**  para incluir impuestos al generar código de seguimiento para la parte de comercio electrónico.
* Marque la casilla de verificación **Incluir ID de cliente** para incluir el identificador del cliente en el script.

Haga clic en **Guardar**. Google Analytics se integrará en tu tienda.

