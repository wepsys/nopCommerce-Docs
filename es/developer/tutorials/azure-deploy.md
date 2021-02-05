---
title: Step by step to deploy on Azure with GIT and automatic builds
uid: en/developer/tutorials/azure-deploy
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

## Paso a paso para implementar en Azure con GIT y compilaciones automáticas

## Guía paso a paso para la implementación automática de nopCommerce con git en azure

1. **Tu propio repositorio git** Necesitas tu propio repositorio, no puedes simplemente construir nopCommerce. Está diseñado para usarse con la función "Publicar" en Visual Studio 2017 de forma predeterminada. Yo mismo uso Bitbucket y lo mantengo sincronizado con el repositorio oficial.

1. Configurar git en Azure
    - Tutorial:[https://azure.microsoft.com/da-dk/documentation/articles/web-sites-publish-source-control/](https://azure.microsoft.com/da-dk/documentation/artículos/sitiosweb-publicación-control-fuente/)

    - Aquí hay un gran video: [http://channel9.msdn.com/Shows/Azure-Friday/What-is-Kudu-Azure-Web-Sites-Deployment-with-David-Ebbo](http://channel9.msdn.com/Shows/Azure-Friday/What-is-Kudu-Azure-Web-Sites-Deployment-with-David-Ebbo)

1. **Prepárese para la implementación local** Cuando se aseguró de que la compilación automática funciona, estamos listos para personalizar nuestros scripts de implementación. Esto es necesario porque la compilación automática predeterminada solo compila proyectos `nop.web`. El problema con esto es que no crea el sitio web de administración y ninguno de los complementos está construido. No puede hacer referencia a los complementos, ya que crearía referencias circulares. Así que ahora necesitamos que la compilación personalizada funcione, estos son los pasos de instalación (también mencione otros lugares)
    - Instale NodeJs: [https://nodejs.org](https://nodejs.org)

    - Instale la CLI de Azure: [https://azure.microsoft.com/documentation/articles/xplat-cli-install/](https://azure.microsoft.com/documentation/articles/xplat-cli-install/)

1. **Hacer que NuGet funcione en el nivel de la línea de comandos.** El comportamiento predeterminado del script KUDO es buscar paquetes NuGet.
   - Para obtener acceso al archivo `Nuget.exe`, puede descargarlo desde aquí: [https://docs.nuget.org/consume/command-line-reference](https://docs.nuget.org/consume/ referencia de línea de comandos). También puede "Habilitar la restauración automática de paquetes NuGet" en Visual Studio 2017, y se agregará a su proyecto automáticamente.

   - Asegúrese de que NuGet esté en la RUTA. Copie el archiv o `nuget.exe` a la ubicación preferida (yo uso`c:/Archivos de programa/ Nuget/Nuget.exe`). Agréguelo a la variable de entorno PATH.
   - Confirme que NuGet está en su RUTA iniciando `cmd.exe` y escriba *nuget*. debería ver las opciones de comando.

1. **Genere scripts de implementación localmente**
    - Abra el "Símbolo del sistema de Microsoft Azure"
    - Navegue a la carpeta src de su proyecto como lo haría normalmente en una ventana de shell
    - Ejecute el generador de scripts azure (encontré este interesante tutorial: [http://blog.amitapple.com/post/38418009331/azurewebsitecustomdeploymentpart2/#.VWyO3qikLjQ](http://blog.amitapple.com/post/38418009331/azurewebsitecustomdep#.VWyO3qikLjQ)).

        Entonces escribirías algo como:

        `azure site deploymentscript --aspWAP Presentation\Nop.Web\Nop.Web.csproj -s NopCommerce.sln`
    - Verifique que haya generado 2 archivos (en la raíz de su repositorio local):

`.deployment`
`deploy.cmd`

1. **Ejecutar el script generado**
    - Debes mantener el archivo .deployment y deploy.cmd en la raíz del repositorio de git
    - Edite deploy.cmd ya que la variable `% DEPLOYMENT_SOURCE%` contiene la raíz del repositorio de git. Entonces agregaría 
     `%DEPLOYMENT_SOURCE%\src\Presentation\Nop.Web\Nop.Web.csproj` en lugar de`%DEPLOYMENT_SOURCE%\Presentation\Nop.Web\Nop.Web.csproj`. Todas las rutas en la sección de implementación deben corregirse.
    - Ejecute deploy.cmd para ver si el script de implementación predeterminado funciona localmente. Debería crear una carpeta\artifact   justo fuera de su repositorio de git.

1. **Personaliza el script de implementación** Así que ahora estamos en la parte final: sonríe :. Aquí es donde todo ese trabajo vale la pena: sonríe :. Queremos alterar la siguiente pieza:

    ```sh
    ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
    :: Deployment
    :: ----------echo Handling .NET Web Application deployment.
    :: 1. Restaurar paquetes de NuGet
    IF /I "NopCommerce.sln" NEQ "" (
    call :ExecuteCmd nuget restore "%DEPLOYMENT_SOURCE%\NopCommerce.sln"
    IF !ERRORLEVEL! NEQ 0 goto error
    )
    :: 2. Construir para el camino temporal
    IF /I "%IN_PLACE_DEPLOYMENT%" NEQ "1" (
    call :ExecuteCmd "%MSBUILD_PATH%" "%DEPLOYMENT_SOURCE%\Presentation\Nop.Web\Nop.Web.csproj" /nologo /verbosity:m /t:Build /t:pipelinePreDeployCopyAllFilesToOneFolder /p:_PackageTempDir="%DEPLOYMENT_TEMP%";AutoParameterizationWebConfigConnectionStrings=false;Configuration=Release /p:SolutionDir="%DEPLOYMENT_SOURCE%\.\\" %SCM_BUILD_ARGS%
    ) ELSE (
    call :ExecuteCmd "%MSBUILD_PATH%" "%DEPLOYMENT_SOURCE%\Presentation\Nop.Web\Nop.Web.csproj" /nologo /verbosity:m /t:Build /p:AutoParameterizationWebConfigConnectionStrings=false;Configuration=Release /p:SolutionDir="%DEPLOYMENT_SOURCE%\.\\" %SCM_BUILD_ARGS%
    )
    IF !ERRORLEVEL! NEQ 0 goto error
    :: 3. KuduSync
    IF /I "%IN_PLACE_DEPLOYMENT%" NEQ "1" (
    call :ExecuteCmd "%KUDU_SYNC_CMD%" -v 50 -f "%DEPLOYMENT_TEMP%" -t "%DEPLOYMENT_TARGET%" -n "%NEXT_MANIFEST_PATH%" -p "%PREVIOUS_MANIFEST_PATH%" -i ".git;.hg;.deployment;deploy.cmd"
    IF !ERRORLEVEL! NEQ 0 goto error
    )
    ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
    ```

    Así que entre no :: 1 y :: 2 ahí es donde colocaremos nuestros comandos para construir complementos.

Un ejemplo del primer complemento sería:

    ```sh
    :: 1.01 Cree roles de cliente de complemento en una ruta temporal
    call :ExecuteCmd "%MSBUILD_PATH%" "%DEPLOYMENT_SOURCE%\src\Plugins\Nop.Plugin.DiscountRules.CustomerRoles\Nop.Plugin.DiscountRules.CustomerRoles.csproj"/nologo/verbosity:m/t:Build/p:AutoParameterizationWebConfigConnectionStrings=false;Configuration=Release/p:SolutionDir="%DEPLOYMENT_SOURCE%\.\\"%SCM_BUILD_ARGS%
    ```

Ahora el complemento está construido cuando ejecuta los scripts de implementación :)
