---
title: How to deploy nopCommerce to Azure
uid: en/developer/tutorials/azure-publish
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Cómo implementar nopCommerce en Azure

## Crear una máquina virtual en Azure

Esta instrucción de los pasos necesarios para configurar una máquina virtual de Azure para hospedar aplicaciones web de nopCommerce y permitir que se publiquen mediante WebDeploy.

### Crear una nueva máquina virtual

1. Inicie sesión en [AzurePortal](https://portal.azure.com/)
1. Haga clic en el botón  **Agregar**

    ![azure-publish_1](_static/azure-publish/azure-publish_1.png)

1. Seleccione  *Windows Server 2016 VM*  en la categoría *Get Started*  o cualquier Windows Server 2016 en la categoría Compute, como  **Windows Server 2016 Datacenter**
1. Complete los campos necesarios para configurar la nueva máquina virtual.
    - Nombre de usuario/contraseña. Lo necesitará para acceder a la máquina virtual. Esta es la cuenta de administrador para conectarse en la máquina virtual mediante RDP.
    - Grupo de recursos. Este es el nombre de la "carpeta virtual" que contiene todos los recursos creados para esta máquina virtual. Puede eliminar todos los recursos creados durante este proceso eliminando el grupo de recursos.

### Configurar componentes y características en la máquina virtual

1. Nombre DNS:
    - Desde [AzurePortal](https://portal.azure.com/), vaya a la página Información general de la máquinavirtual.
    - En Nombre DNS, haga clic en  **Configurar**
    - Proporcionar un nombre DNS único a nivel mundial. (Una marca verde aparece cuando se valida el nombre.)
    - Haga clic en  **Guardar**  para guardar la configuración.

### Configurar reglas de Azure Firewall

1. Configure las reglas de firewall de entrada en Azure Portal. En la sección Redes, agregue la regla de puerto de entrada para crear nuevas entradas de firewall:
    - http - Puerto 80 (Prioridad 100)
    - WebDeploy - Puerto 8172 (Prioridad 1010)
    - RDP - Puerto 3389 (Prioridad 320)

    ![azure-publish_2](_static/azure-publish/azure-publish_2.png)

2. Configure las reglas de firewall saliente en Azure Portal. En la sección Redes, agregue la regla de puerto de salida para crear nuevas entradas de firewall:
    - RDP - Puerto 3389 (Prioridad 100)

## Conéctese a la máquina virtual (RDP) mediante el inicio de sesión y la contraseña

![azure-publish_3](_static/azure-publish/azure-publish_3.png)

### Instalar IIS (servidor web) y ASP.NET 4.6

1. Abra el panel del administrador del servidor ** (administrador del servidor - el panel se abre en el primer inicio)
1. Elija  **2 Añadir roles y características**

![azure-publish_4](_static/azure-publish/azure-publish_4.png)

1. Acepte los valores predeterminados y presione  **Next**  tres veces para avanzar a la sección Roles de servidor.
1. Seleccione  **Servidor Web (IIS)**

![azure-publish_5](_static/azure-publish/azure-publish_5.png)

1. Cuando se le solicite, confirme la instalación adicional de  *IIS Management Console*.
1. Presione  **Next**  tres veces para avanzar a la  sección *Web Server Role (IIS) --> Roles Services*
1. Seleccione el servicio de administración, que es necesario para habilitar Web Deploy (a través del puerto 8172). Cuando se le solicite, confirme la instalación adicional de ASP.NET 4.6.

    ![azure-publish_6](_static/azure-publish/azure-publish_6.png)

1. Seleccione  **Next**  para confirmar la configuración y, a continuación,  **Instalar**  para completar la instalación de IIS.

    ![azure-publish_7](_static/azure-publish/azure-publish_7.png)

Una vez completada la instalación:
    - IIS se instala y se ejecuta con la regla de firewall interna creada para el puerto 80.
    - El servicio de administración web se instala con la regla de firewall interno creada para el puerto 8172.

### Configurar la seguridad mejorada de IE (desactivado)

En una nueva máquina virtual de Azure, las reglas de seguridad predeterminadas impiden que los ejecutables se descarguen a través de Internet Explorer. Para descargar el ejecutable de WebDeploy, primero debe deshabilitar la seguridad mejorada de IE.

1. En el  **Server Manager**, abrala sección **Local Server**  a la izquierda.
1. En el panel principal, junto a "**IE Enhanced Security Configuration:**", seleccione On.
1. En el cuadro de diálogo que aparece, seleccione  **Off para Administradores**,seleccione  **Activado para Usuarios**y, a continuación, seleccione  **OK**.

    ![azure-publish_8](_static/azure-publish/azure-publish_8.png)

### Instalar Web Deploy

1. Inicie Internet Explorer.
1. Acepte la configuración de seguridad predeterminada.
1. [Descargar](https://www.microsoft.com/download/details.aspx?id=43717)  *WebDeploy_amd64_en-US.msi*
1. Siga los pasos de instalación para Web Deploy
1. Elija la opción Completar para instalar todos los componentes

### Instalar la última versión [SDK de NET Core](https://www.microsoft.com/net/download/all)

### Instalar paquete [.NET Core Windows Server Hosting](https://www.microsoft.com/net/download/all)

![azure-publish_9](_static/azure-publish/azure-publish_9.png)

IIS se utiliza para hospedar ASP.NET aplicaciones web principales, su rol se reducirá a un servidor proxy. El hospedaje de aplicaciones ASP.NET Core en IIS se produce mediante el AspNetCoreModule nativo, que está configurado para redirigir las solicitudes al servidor web de Kestrel. Este módulo controla el inicio del proceso externo `dotnet.exe`, dentro del cual se hospeda la aplicación, y reenvía todas las solicitudes de IIS a este proceso de host.

Después de instalar este paquete, ejecute el comando **iisreset**  en la línea de comandos o reinicie IIS manualmente para que el servidor aplique los cambios.

### Configurar IIS

1. Debe conceder permiso a la carpeta wwwroot. Con el sitio seleccionado en el Administrador de IIS ,elija  **Editar permisos**y asegúrese de que  *IUSR*,  *IIS_IUSRS*o el usuario configurado para el grupo de aplicaciones es un usuario autorizado con derechos de lectura y ejecución. Si ninguno de estos usuarios está presente, agregue  *IUSR*  como usuario con los derechos *Read &  Execute*.

![azure-publish_10](_static/azure-publish/azure-publish_10.png)

1. Haga clic en Reiniciar en el  panel derecho para reiniciar IIS

Ahora todo está listo para publicar el proyecto.

## Publicar nopCommerce en una máquina virtual de Azure desde Visual Studio

Publicar la aplicación nopCommerce no es diferente de publicar cualquier otra aplicación ASP.NET Core. Por lo tanto, se describirán los requisitos mínimos para ejecutar la publicación. Puede encontrar más detalles [aquí](https://docs.microsoft.com/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?view=aspnetcore-2.1#deploy-the-app-to-azure).

### Publicar el proyecto 'Nop.Web'

1. Abra la solución de aplicación web en Visual Studio 2017. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y elija  *Publicar*.

![azure-publish_11](_static/azure-publish/azure-publish_11.png)

1. Utilice la flecha a la derecha de la página para desplazarse por las opciones de publicación hasta que encuentre  **Microsoft Azure Virtual Machines**. Seleccione la máquina virtual adecuada en la lista de Máquinas virtuales existentes.
1. Haga clic en Crear perfil..

![azure-publish_12](_static/azure-publish/azure-publish_12.png)

1. Para ver y modificar la configuración del perfil de publicación, seleccione  **Configurar**. Utilice el botón Validar conexión para confirmar que ha introducido la información correcta.

![azure-publish_13](_static/azure-publish/azure-publish_13.png)

1. Si desea asegurarse de que el servidor web tiene una copia limpia de la aplicación web después de cada carga (y que no quedan otros archivos colgados de una implementación anterior), puede marcar la casilla de verificación  **Eliminar archivos adicionales en destino** en la pestaña **Configuración**  Advertencia: Publicar con esta configuración elimina todos los archivos que existen en el servidor web (directorio wwwroot). Asegúrese de conocer el estado de la máquina antes de publicar con esta opción habilitada.

![azure-publish_14](_static/azure-publish/azure-publish_14.png)

1. Haga clic en  **Guardar**.
1. Haga clic en  **Publicar**  para comenzar a publicar.

Ahora ha publicado la aplicación web en una máquina virtual de Azure.You have published your web app to an Azure virtual machine.

## Problemas y soluciones potenciales

Para [más](https://docs.microsoft.com/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-2.0) entender con precisión cuál esel problema, usted necesita habilitar el registro - stdoutLog habilitado en el web.config:

````sh
stdoutLogEnabled" ``true`stdoutLogFile=".\logs\stdout"
```

## IIS no puede localizar el web.config

Solución: [support.microsoft.com](http://support.microsoft.com/kb/942055)
