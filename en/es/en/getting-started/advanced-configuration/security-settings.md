---
title: Security settings
uid: en/getting-started/advanced-configuration/security-settings
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.ivkadp, git.mariannk
---

 # Configuración de seguridad

Para administrar la configuración de seguridad, vaya a **Configuración > Configuración > Configuración general**.

Esta página habilita la configuración de varias tiendas, significa que se puede definir la misma configuración para todas las tiendas o diferir de una tienda a otra. Si desea administrar la configuración de una tienda determinada, elija su nombre en la lista desplegable de configuración de varias tiendas y marque todas las casillas de verificación necesarias en el lado izquierdo para establecer el valor personalizado para ellos. Para obtener más información, consulte [Multi-store](xref:en/getting-started/advanced-configuration/multi-store).

# Seguridad

Defina la configuración de *Seguridad* de  la siguiente manera:
![Seguridad](_static/security-settings/security.jpg)

* En el campo IP permitida del área de administración, introduzca las direcciones IP que pueden acceder al back-end. Deje este campo vacío si no desea restringir el acceso al back-end. Utilice comas entre las direcciones IP (por ejemplo, 127.0.0.10, 232.18.204.16).
* Marque el  **Habilitar honeypot**  para habilitar [honeypot](https://es.wikipedia.org/wiki/Honeypot_(computing)). En terminología informática, un honeypot es una trampa establecida para detectar, desviar o, de alguna manera, contrarrestar los intentos de uso no autorizado de los sistemas de información.
* En el campo **Encryption private key**,  introduzca la clave privada de cifrado utilizada para almacenar datos confidenciales. Haga clic en  **Cambiar**  en cualquier momento para cambiar esta clave. Todos los datos confidenciales se cifran con esta clave privada.

> [!NOTA]
>
> Se recomienda hacer una copia de seguridad de la base de datos antes de cambiar la clave de cifrado. Los datos confidenciales incluyen toda la información de la tarjeta de crédito (solo cuando esta información de la tarjeta de crédito se almacena en la base de datos de la tienda).

# CAPTCHA

CAPTCHA es un programa que puede saber si es un humano o un ordenador está tratando de acceder a su sitio web. nopCommerce utiliza reCAPTCHA de Google. reCAPTCHA es un servicio gratuito que protege su sitio web de spam y abuso. reCAPTCHA utiliza un motor de análisis de riesgos avanzado y desafíos adaptativos para evitar que el software automatizado participe en actividades abusivas en su sitio. Lo hace mientras permite que sus usuarios válidos pasen con facilidad.

Defina la configuración de *CAPTCHA* de  la siguiente manera:
![CAPTCHA](_static/security-settings/captcha.jpg)

Este panel revelará los siguientes ajustes cuando se marque **CAPTCHA  habilitado**:
* **Tipo de reCAPTCHA**: elija reCAPTCHA v2 o reCAPTCHA v3. La diferencia entre ellos es que reCAPTCHA v2 muestra la casilla de verificación "No soy un robot", pero reCAPTCHA v3 es invisible para los clientes. Leer más sobre [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)y [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3).
* **reCAPTCHA v3 umbral de puntuación**  se habilita cuando se selecciona reCAPTCHA v3. Leer más sobre el umbral de puntuación [aquí](https://developers.google.com/recaptcha/docs/v3).
* Mostrar CAPTCHA en la página **login**.  
* Mostrar CAPTCHA en la página de registro ***.  
* Mostrar CAPTCHA en la página **olvidé la contraseña**.  
* Mostrar CAPTCHA en la página **Contáctenos**.  
* Mostrar CAPTCHA en la lista de deseos de correo electrónico a un amigo **  página.
* Mostrar CAPTCHA en el  ** producto de correo electrónico a un amigo **  página.
* Mostrar CAPTCHA en la página de blog *****.
* Mostrar CAPTCHA en la página de noticias (comentarios)**.
* Mostrar CAPTCHA en la página **revisiones de productos**.  
* Mostrar CAPTCHA en la página **aplicar para la cuenta de proveedor**.  
* Mostrar CAPTCHA en la página **foro**.  
* Introduzca el reCAPTCHA  **clave pública**.
* Introduzca la clave de reCAPTCHA  **privada**.

> [!NOTA]
>
> Se ha eliminado la compatibilidad con Recaptcha v1.


