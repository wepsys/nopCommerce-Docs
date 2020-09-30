---
title: External authentication methods
uid: en/getting-started/advanced-configuration/external-authentication-methods
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Métodos de autenticación externa

Los métodos de autenticación externa permiten a los usuarios iniciar sesión en un sitio de nopCommerce sin introducir sus credenciales: correo electrónico y contraseña. Los usuarios se pueden autenticar mediante un sitio externo (como Facebook, Google, etc.). nopCommerce tiene una autenticación externa integrada a través de Facebook. Puede configurar otros métodos utilizando plugins de [marketplace](https://www.nopcommerce.com/marketplace).

Después de configurar y marcar un método de autenticación externo como activo, los usuarios verán una nueva opción de autenticación en la página de inicio de sesión.

# Administrar los métodos de autenticación externa

Ir a **Configuración > Autenticación externa**. Aparece la ventana *Autenticación externa*:  

![Autenticación externa](_static/external-authentication-methods/external-authentication.png)

Haga clic en Editar junto  a un método de autenticación y marque  **Está activo para activar el método. También puede definir el método  **Mostrar orden**. A continuación, haga clic en el botón **Actualizar**  para guardar los cambios.

Haga clic en Configurar para la configuración del método.

# Administrar la autenticación de Facebook

El método de autenticación de Facebook es un complemento de autenticación externa integrado. Para configurar la autenticación con Facebook, sigue estos pasos:

1. En la página **Configuración > Autenticación externa**  haga clic en  **Configurar**  junto a la  autenticación de Facebook.*. Se muestra la ventana *Configurar - Autenticación de Facebook*:  

![Facebook](_static/external-authentication-methods/facebook.jpg)

1. Vaya a lapágina [ Facebook paradesarrolladores](https://developers.facebook.com/apps) e iniciesesión. Si aún no tienes una cuenta de Facebook, usa el enlace Registrarse en Facebook en la página de inicio de sesión para crear una.
1. Toque el  botón **+ Agregar una nueva aplicación**  en la esquina superior derecha para crear un nuevo ID de aplicación. (Si esta es su primera aplicación con Facebook, el texto del botón será  **Crear una nueva aplicación**.)
1. Rellene el formulario y toque el  botón Crear ID de aplicación**.
1. Se muestra la página *Configuración del producto*, que le permite seleccionar las características de su nueva aplicación.  **Get Started**   *Facebook Login*.
1. Haga clic en el enlace **Configuración**  en el menú de la izquierda, se le presentará la página *Configuración de OAuth de cliente*  con algunos valores predeterminados ya establecidos.
1. Introduzca  'https://yoursitename.com/signin-facebook' en el campo URI de redirección de OAuth válidos que  reemplaza  a `yoursitename.com`  woth su URL de sitio.
1. Haga clic en  **Guardar cambios**.
1. Haga clic en el enlace **Dashboard**  en el panel de navegación izquierdo.
1. Copie su  **App ID/API Key**  y  **App secret** en el formulario en la página de configuración del plugin.

Haga clic en el botón Guardar.guardar.  En la página de inicio de sesión del almacén público, consulte el método de autenticación recién agregado.

# Véase también

* [Plugins en nopCommerce](xref:en/getting-started/advanced-configuration/plugins-in-nopcommerce)


