---
title: GDPR settings
uid: en/getting-started/advanced-configuration/gdpr-settings
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.ivkadp, git.mariannk
---

# Configuración del RGPD

*GDPR* (Reglamento General de Protección de Datos) es una nueva ley de privacidad de datos revisada de la Unión Europea que afecta a la forma en que todas las empresas recopilan, utilizan y comparten datos personales de sus clientes europeos. El Reglamento entró en vigor el 24 de mayo de 2016 y se aplica desde el 25 de mayo de 2018. El Reglamento es un paso esencial para reforzar los derechos fundamentales de las personas en la era digital y facilitar las empresas mediante la clarificación de las normas para las empresas y los organismos públicos en el mercado único digital.

Para obtener más información (consulte esta fuente):

[https://ec.europa.eu/info/law/law-topic/data-protection/data-protection-eu_en](https://ec.europa.eu/info/law/law-topic/data-protection/data-protection-eu_en)

# Configurar el RGPD

Para activar la configuración del RGPD en tu tienda de nopCommerce, ve a **Administración > Configuración > Configuración > Ajustes del RGPD**.

![Configurar](_static/gdpr-settings/configure.jpg)

A continuación, marque la casilla de verificación **GDPR enabled**.  La configuración adicional le permitirá capturar un registro de las siguientes actividades:

* **Registro "aceptar política de privacidad" consentimiento**.
* **Registrar el consentimiento de "newsletter"**.
* **Registrar cambios de perfil de usuario**.

Puedes añadir consentimientos en tu sitio de nopCommerce haciendo clic en el botón  **Agregar consentimiento en el panel *Consentimientos*:  

![Consentimientos](_static/gdpr-settings/consents.jpg)

Para añadir un nuevo consentimiento, se le redirigirá a la ventana *Agregar consentimiento*:  

![Añadir consentimiento](_static/gdpr-settings/add-consent.jpg)

Defina la siguiente configuración de consentimiento:

* **Mensaje**  o pregunta que se mostrará a los clientes.
* Si se requiere el consentimiento  **Se requiere**.
* Si el consentimiento será  **Mostrado durante el registro**.
* Si el consentimiento se mostrará en la página "Información del cliente"**  en la sección "Mi cuenta".
* **El pedido de visualización**  es el orden de visualización del consentimiento. 1 representa el primer elemento de la lista.

Aquí está un ejemplo de una opción de consentimiento en la página de información del cliente:

![acuerdo](_static/gdpr-settings/agreement.png)

Si ha habilitado la configuración del registro de consentimiento, puede ver la actividad del registro yendo a: **Administración: Clientes, Solicitudes GDPR (log)**.

![log](_static/gdpr-settings/log.png)

Cuando la configuración del RGPD está habilitada, el propietario de la tienda también puede realizar acciones como:

* **Eliminación permanente**  para la eliminación del registro del cliente.
* **Exportar datos**  para exportar datos de clientes.

Para ello, vaya a la página **Administración > Clientes > Editar cliente**.  

![customerdetails](_static/gdpr-settings/customerdetails.png)

# Tutoriales

* [Gestión de la configuración del RGPD en nopCommerce](https://www.youtube.com/watch?v=6bLc_TDqD18&feature=youtu.be)


