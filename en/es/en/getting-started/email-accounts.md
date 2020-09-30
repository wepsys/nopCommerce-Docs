---
title: Email accounts
uid: en/getting-started/email-accounts
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Cuentas de correo electrónico

Este capítulo describe cómo configurar las cuentas de correo electrónico asociadas a su tienda: un correo electrónico de contacto general, un correo electrónico de representante de ventas, un correo electrónico de asistencia al cliente y más.

Para administrar las cuentas de correo electrónico, vaya a **Configuración → Cuentas de correo electrónico**. La ventana *Cuentas de correo electrónico* muestra las cuentas de correo electrónico del propietario de la tienda, como se muestra a continuación. Una vez configuradas las cuentas de correo electrónico, el propietario de la tienda puede seleccionar la cuenta de correo electrónico necesaria en la página de detalles de la plantilla de mensajes, como se describe en la sección [Message templates](xref:en/running-your-store/content-management/message-templates) chapter.

![Email accounts](_static/email-accounts/email-accounts.png)

## Agregar una nueva cuenta de correo electrónico

Para añadir una nueva cuenta de correo electrónico haga clic en **Añadir nuevo**. Aparecerá la ventana *Añadir una nueva cuenta de correo electrónico*:

![Add a new email account](_static/email-accounts/email-accounts-add-new.png)

Defina la siguiente información de la cuenta de correo electrónico:

* En el campo **Dirección de correo electrónico** introduzca la dirección de correo electrónico de origen para todos los correos electrónicos salientes de su tienda. Por ejemplo, `sales@yourstore.com`.
* En el campo **Nombre de visualización de correo electrónico**, introduzca el nombre que se muestra para los correos electrónicos salientes de su tienda. Ejemplo: "El departamento de ventas de tu tienda".
* En el campo **Host**, introduzca el nombre de host de la dirección IP de su servidor de correo electrónico.
* En el campo **Puerto**, introduzca el puerto SMTP de su servidor de correo electrónico.
* En el campo **Usuario**, ingrese el nombre de usuario de su servidor de correo electrónico.
* En el campo **Contraseña**, introduzca la contraseña de su servidor de correo electrónico.
* Seleccione la casilla de verificación **SLL**, para usar la Capa de Sockets de Seguridad para encriptar la conexión SMTP.
* Seleccione la casilla de verificación **Use default credentials**, para utilizar las credenciales predeterminadas para la conexión.

Haga clic en **Guardar**. La ventana se expande, de la siguiente manera:

![Email account  - Details](_static/email-accounts/email-accounts-details.png)

En el campo **Enviar correo electrónico a**, introduzca la dirección de correo electrónico del correo electrónico de prueba y haga clic en **Enviar correo electrónico de prueba**.
