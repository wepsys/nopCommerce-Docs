---
title: Installing local
uid: en/installation-and-upgrading/installing-nopcommerce/installing-local
author: git.AndreiMaz
contributors: git.IvanIvanIvanov, git.mariannk
---

# Inscontando local

Este capítulo describe cómo descargar el software nopCommerce, cargarlo en su servidor, definir los permisos de archivo e instalarlo en su sistema. También puede ver el screencast sobre la instalación de nopCommerce en nuestro [canal de YouTube](https://www.youtube.com/watch?v=L7NGodeB9sQ).

Antes de comenzar la instalación, asegúrese de que su servidor web tenga los [requisitos mínimos para ejecutar nopCommerce](xref:en/installation-and-upgrade/technology-and-system-requirements).

> [!NOTA]
> Para obtener más información sobre las pautas de selección de alojamiento, visite [esta página](xref:en/installation-and-upgrade/installation-nopcommerce/choose-a-hosting-company).

Hay varias opciones disponibles al descargar nopCommerce. Para determinar qué opción descargar, debe decidir cómo la usará. Las siguientes opciones están disponibles:
1. **Web (sin fuente)**. Esta opción está disponible para usuarios que no deseen/necesiten desarrollar ningún código personalizado. Esta es una versión precompilada de nopCommerce que simplemente puede cargarse en su proveedor de alojamiento y usarse de inmediato. Con esta opción, los usuarios aún pueden modificar la apariencia o la interfaz de usuario (UI) de su sitio para satisfacer sus necesidades, pero no tienen que preocuparse por el desarrollo.
1. **Código fuente**. Esta opción contiene una solución completa de Visual Studio. Es para usuarios que desean personalizar el código dentro de nopCommerce. Contiene todo el código fuente utilizado para desarrollar nopCommerce y debe abrirse en Visual Studio. También incluye scripts para crear y compilar la solución para cargarla en su proveedor de alojamiento.
1. **Script de actualización**. La opción de script de actualización es para usuarios que ya tienen instalada una instalación de nopCommerce. El script actualizará su instalación actual a la última versión.

Con cada una de estas opciones, excluyendo el script de actualización, puede implementar nopCommerce en su entorno de desarrollo y su proveedor de alojamiento. Elija la opción que le gustaría [descargar](https://www.nopcommerce.com/en/download-nopcommerce) y haga clic en el enlace de descarga correspondiente para comenzar su descarga. Se recomienda que cree una nueva carpeta en su escritorio para almacenar sus archivos descargados para un fácil acceso.


## Ejecutando el sitio usando IIS (paquete sin código fuente)

Para usar IIS, copie el contenido de la carpeta nopCommerce extraída en un directorio virtual de IIS (o raíz del sitio) y luego vea el sitio usando un navegador.

Si está utilizando nopCommerce 3.90 y versiones anteriores, configúrelo para que se ejecute en modo integrado y configure el grupo de aplicaciones para ejecutar .NET Framework versión 4. Tenga en cuenta que no es necesario para nopCommerce 4.00 y versiones posteriores.


## Ejecutando el sitio usando Visual Studio (paquete con código fuente)

Este paso describe cómo iniciar un sitio en Visual Studio. Para ejecutar el sitio en Visual Studio, extraiga el archivo de código fuente completo en una carpeta local. Inicie Visual Studio y seleccione **Archivo→ Abrir →Proyecto/Solución**. Navegue a la carpeta donde extrajo el archivo y abra el archivo de solución `NopCommerce.sln`. Ejecute el proyecto `Nop.Web`.


## Obtener el paquete "listo para implementar" (sin código fuente) de un paquete con código fuente

Si está utilizando nopCommerce **3.20 (o superior)**, siga los siguientes pasos:
* Abra la solución en Visual Studio.
* Reconstruir toda la solución.
* Publique el proyecto **Nop.Web** de Visual Studio. Al publicar, asegúrese de que la configuración esté establecida en *Release*.


## Proceso de instalación ##

nopCommerce requiere permisos de escritura para los directorios y archivos que se describen a continuación:

- **For nopCommerce versions 4.00 and above:**
  - `\App_Data\`
  - `\bin\`
  - `\log\`
  - `\Plugins\`
  - `\Plugins\bin\`
  - `\wwwroot\bin\`
  - `\wwwroot\bundles\`
  - `\wwwroot\db_backups\`
  - `\wwwroot\files\exportimport\`
  - `\wwwroot\images\`
  - `\wwwroot\images\thumbs\`
  - `\wwwroot\images\uploaded`
  - `\App_Data\Plugins.json` (after installation)
  - `\App_Data\dataSettings.json` (after installation)

- **For nopCommerce versions 2.00-3.90:**
  - `\App_Data\`
  - `\bin\`
  - `\Content\`
  - `\Content\Images\`
  - `\Content\Images\Thumbs\`
  - `\Content\Images\Uploaded\`
  - `\Content\files\ExportImport\`
  - `\Plugins\`
  - `\Plugins\bin\`
  - `\Global.asax`
  - `\web.config`

Estos permisos se validan durante el proceso de instalación. Si no tiene permisos de escritura, se muestra un mensaje de advertencia solicitándole que configure los permisos.
Antes de instalar nopCommerce, asegúrese de tener instalado el servidor de base de datos en su sistema.

Puede utilizar cualquiera de los siguientes métodos de autenticación para conectarse al servidor:
* **Cuenta de servidor SQL**: cuando se conecta mediante este método, los inicios de sesión se crean en el servidor SQL que no se basa en las cuentas de usuario de Windows. Tanto el nombre de usuario como la contraseña se crean utilizando el servidor SQL y se almacenan en el servidor SQL. Al usar este método, debe ingresar su nombre de usuario y contraseña.
* **Autenticación de Windows integrada**: cuando se conecta mediante este método, SQL Server valida el nombre de la cuenta y la contraseña mediante el token principal de Windows en el sistema operativo. Esto significa que Windows confirma la identidad del usuario. SQL Server no solicita una contraseña y no realiza la validación de identidad. La autenticación de Windows es el modo de autenticación predeterminado y es mucho más seguro que la autenticación del servidor SQL. La autenticación de Windows utiliza el protocolo de seguridad Kerberos, proporciona la aplicación de la política de contraseñas con respecto a la validación de la complejidad para contraseñas seguras, brinda soporte para el bloqueo de cuentas y admite la caducidad de contraseñas. Una conexión realizada mediante la autenticación de Windows a veces se denomina conexión de confianza, porque el servidor SQL confía en las credenciales proporcionadas por Windows.

Una vez que abra el sitio por primera vez, será redirigido a la página de instalación, de la siguiente manera:
![instalación de nopCommerce](_static/installation-local/installation.jpg)

En el panel *Información de la tienda*, complete los siguientes detalles:
* **Correo electrónico del usuario administrador**: esta es la dirección de correo electrónico del primer administrador del sitio.
* **Contraseña de usuario administrador**: deberá proporcionar una contraseña para la cuenta de administrador.
* **Confirme la contraseña**: confirme la contraseña del usuario administrador.
* **Crear datos de muestra**: marque esta casilla de verificación si desea que se creen productos de muestra. Esto se recomienda para que pueda comenzar a trabajar con su sitio antes de agregar cualquiera de sus propios productos. Siempre puede eliminar estos elementos más tarde o anular la publicación para que dejen de aparecer en su sitio.

En el panel *Información de la base de datos* debe ingresar la siguiente información:
* **Base de datos**: aquí puede seleccionar Microsoft SQL Server o MySQL.
* **Cree una base de datos si no existe**: se recomienda que cree su base de datos y el usuario de la base de datos de antemano para garantizar una instalación exitosa. Simplemente cree una instancia de base de datos y agregue el usuario de la base de datos. El proceso de instalación creará todas las tablas, procedimientos almacenados, etc.
* **Ingrese una cadena de conexión sin procesar (avanzado)**: marque esta casilla de verificación si desea ingresar una ** Cadena de conexión ** en lugar de completar los campos de conexión.
* **Nombre del servidor**: esta es la IP, URL o nombre del servidor de su base de datos. Obtenga el nombre de su servidor del sistema de administración de la base de datos o del panel de control de alojamiento.
* **Nombre de la base de datos**: este es el nombre de la base de datos utilizada por nopCommerce. Si optó por crear su base de datos con anticipación, use el nombre que le dio a su base de datos aquí.
* **Use la autenticación de Windows integrada**: si está instalando en un proveedor de alojamiento, puede usar su cuenta de SQL Server y proporcionar las credenciales que creó con su base de datos. En este caso, no hackear esta opción. Si está utilizando un entorno de desarrollo, puede seleccionar la autenticación de Windows. En este caso, marque esta casilla de verificación. Si utiliza la autenticación de Windows, la cuenta que aloja el grupo de aplicaciones en IIS debe ser un usuario de la base de datos.
* **Nombre de usuario SQL**: ingrese su nombre de usuario de la base de datos.
* **SQL Password**: ingrese su contraseña de usuario de la base de datos.
* **Especificar clasificación personalizada**: esta es una configuración avanzada y debe dejarse sin marcar.

Haga clic en **Instalar** para iniciar el proceso de instalación. Cuando se completa el proceso de configuración, se muestra la página de inicio de su nuevo sitio.

> [!NOTA]
> El botón **Reiniciar la instalación** en la parte inferior de la página de instalación le permite reiniciar el proceso de instalación en caso de que algo salga mal.

> [!NOTA]
> Si está utilizando nopCommerce 3.90 y una versión inferior, asegúrese de que su grupo de aplicaciones esté configurado en modo *Integrado*.

> [!NOTA]
> Si desea restablecer completamente un sitio nopCommerce a su configuración predeterminada, puede eliminar el archivo `dataSettings.json` del directorio` App_Data`. Al usar IIS, es posible que desee leer este artículo.



