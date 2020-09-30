---
title: A guide to expanding the functionality of the basic functions of nopCommerce through a plugin
uid: en/developer/tutorials/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Una guía para ampliar la funcionalidad de las funciones básicas de nopCommerce a través de un plugin

## Overview

nopCommerce utiliza el sistema de plugins para ampliar la funcionalidad del panel de administración de nopCommerce y utiliza el sistema de widgets para ampliar la funcionalidad del sitio web. Los Plugins y Widgets son un conjunto de programas o componentes independientes que pueden ser añadidos a un sistema existente para extender alguna funcionalidad específica y también pueden ser eliminados del sistema sin afectar al sistema principal durante el proceso. Así que usando el concepto de Plugin y Widgets podemos añadir más funcionalidad a nuestro sistema y podemos construirlos sin alterar o editar el código fuente principal de la solución nopCommerce. Lo que nos permite actualizar o bajar nuestra solución nopCommerce a la última versión o a una versión más antigua como deseemos sin tener que reescribir el plugin y los widgets que ya hemos creado.

## Diferencia entre Plugin y Widget

Como sabemos, tanto el plugin como el widget son para ampliar la funcionalidad de la solución nopCommerce. Bueno, entonces puedes preguntarte "¿cuál es la diferencia entre ellos?". En última instancia, en nopCommerce se puede pensar en un widget como un plugin pero con una característica extra. Para crear un widget el proceso es en su mayoría el mismo que el de crear un plugin, pero al usar widget podemos mostrar alguna interfaz de usuario (User Interface) al sitio web público de nopCommerce en algunas áreas específicas predefinidas por nopCommerce que se conoce como widget-zones. Lo cual no podemos lograr sólo a través de un plugin. Puedes pensar que Widget es un superconjunto de Plugin.

Creo que tienes un poco más claro lo que son los widgets y plugins, cuándo se pueden usar y cuáles son los beneficios de usarlos. Así que, ahora vamos a crear un simple widget que muestre el mensaje "Hola Mundo" al sitio público, para entender cómo crear un widget en nopCommerce.

## Iniciar el Proyecto Plugin

### Step 1: Create a new project

Ve a la página web oficial de nopCommerce y descarga el último código fuente de nopCommerce. Como ahora mismo la última versión es la 4.2, esta documentación está escrita según la v4.2. Abre tu solución nopCommerce en tu IDE favorito (se recomienda Visual Studio). Allí verás un montón de carpetas, si quieres saber todo sobre la estructura de carpetas, puedes visitar la documentación de nopCommerce. En el techo de la solución verás una carpeta "Plugins", amplía esa carpeta y verás una lista de los proyectos de plugins que vienen con nopCommerce de forma predeterminada.

![image1](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image1.png)

Para crear un nuevo proyecto de Widget, haga clic con el botón derecho del ratón en la carpeta "Plugins": Add=>Nuevo proyecto. Después de eso aparecerá la ventana de añadir nuevo proyecto.

![image2](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image2.png)

De la lista izquierda de tipo de proyecto seleccione ".NetCore" de que elija "Class Library" proyecto Template. nopCommerce sigue algunos estándares de conversión de nombres, que puede obtener más información de la documentación de nopCommerce. He elegido "Nop.Plugin.Widget.HelloWorld" como nombre de proyecto siguiendo la conversión de nombres de nopCommerce. Y la ubicación debe estar dentro del directorio "/source/Plugins". Ahora haz clic en "OK". Esto debería crear un nuevo proyecto dentro del directorio de Plugins. Y puedes ver en tu solución algo como esto:

![image3](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image3.png)

### Paso 2: Configurar su nuevo proyecto para ser usado como Widget

Necesitamos configurar un par de cosas en nuestro proyecto para que sea usado como un Plugin o Widget.

Después de crear tu proyecto con éxito, abre su archivo .csproj, para ello haz clic con el botón derecho del ratón en tu proyecto y haz clic en el menú {Tu_Nombre_de_proyecto.csproj} del menú de contexto y reemplaza su contenido con el siguiente código.

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>netcoreapp2.2</TargetFramework>
        <Copyright>SOME_COPYRIGHT</Copyright>
        <Company>YOUR_COMPANY</Company>
        <Authors>SOME_AUTHORS</Authors>
        <PackageLicenseUrl>PACKAGE_LICENSE_URL</PackageLicenseUrl>
        <PackageProjectUrl>PACKAGE_PROJECT_URL</PackageProjectUrl>
        <RepositoryUrl>REPOSITORY_URL</RepositoryUrl>
        <RepositoryType>Git</RepositoryType>
        <OutputPath>..\..\Presentation\Nop.Web\Plugins\{PLUGIN_OUTPUT_DIRECTORY}</OutputPath>
        <OutDir>$(OutputPath)</OutDir>
        <!--Set this parameter to true to get the dlls copied from the NuGet cache to the output of your    project. You need to set this parameter to true if your plugin has a nuget package to ensure that   the dlls copied from the NuGet cache to the output of your project-->
        <CopyLocalLockFileAssemblies>false</CopyLocalLockFileAssemblies>
    </PropertyGroup>
    <ItemGroup>
        <ProjectReference Include="..\..\Presentation\Nop.Web.Framework\Nop.Web.Framework.csproj" />
        <ClearPluginAssemblies Include="$(MSBuildProjectDirectory)\..\..\Build\ClearPluginAssemblies.proj" />
    </ItemGroup>
    <!-- This target execute after "Build" target -->
    <Target Name="NopTarget" AfterTargets="Build">
        <!-- Delete unnecessary libraries from plugins path -->
        <MSBuild Projects="@(ClearPluginAssemblies)" Properties="PluginPath=$(MSBuildProjectDirectory)\ $(OutDir)" Targets="NopClear" />
    </Target>
</Project>
```

Aquí sustituye {Plugin_Output_Directory} por el nombre de tu proyecto, en mi caso "Widget.HelloWorld".

Lo que esto hará es copiar todos los archivos dll relacionados con este proyecto en el `Nop.Web/Plugin/{Plugin_Output_Directory}`, porque el directorio de plugins dentro de `Nop.Web` es la ubicación donde nopCommerce busca desde los plugins y widgets para mostrarlos en la lista de plugins o widgets en el panel de administración.

### Paso 3: Crear un archivo Plugin.json

Este archivo es necesario para cada Plugin o Widget que creamos en nopCommerce. Este archivo contiene meta información sobre nuestro plugin que describe nuestro plugin. Contiene información como, Nombre de nuestro plugin, a qué versión de nopCommerce está destinado/construido, alguna descripción sobre nuestro plugin, versión de nuestro plugin y así sucesivamente. Después de crear el archivo "Plugin.json", copie este contenido dentro de su archivo y modifíquelo según sus necesidades.

```json
{
    "Group": "Documents Examples", //Group of Project, this may be your company name
    "FriendlyName": "Hello World", //Friendly Name for your plugin/widget
    "SystemName": "Widget.HelloWorld", //This is unique among all plugins/widgets
    "Version": "1.0", //Version of your Plugin/Widget
    "SupportedVersions": [ "4.20" ], //Version of nopCommerce this Plugin/Widget is supported for. We can add multiple versions, since it is an array.
    "Author": "nopCommerce team", //This can be your name or your Team Name
    "DisplayOrder": 1,
    "FileName": "Nop.Plugin.Widget.HelloWorld.dll", //Output dll file name
    "Description": "This Plugin/Widget is build as an example for nopCommerce documentation." //Short description about your plugin/widget.
}
```

Este archivo es utilizado por nopCommerce mientras se lista nuestro Plugin/Widget en la lista de plugins en el panel de administración y para identificar nuestro plugin de forma única entre todos los plugins instalados y desinstalados en toda la aplicación. Así que para que nopCommerce pueda leer este archivo necesitamos copiarlo en su directorio de salida mientras se construye el proyecto. Para ello, haga clic con el botón derecho del ratón en el archivo Plugin.json y haga clic en la propiedad. En la propiedad, pon el valor de "Copiar en el directorio de salida" en "copiar si es más reciente"


![image4](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image4.png)

### Paso 4: Crear una clase que se extienda desde la clase BasePlugin

En realidad necesitamos tener una clase que sea inherente a la interfaz de IPlugin para que nopCommerce trate nuestro proyecto como un plugin. Pero nopCommerce ya tiene una clase "BasePlugin" que hereda de la interfaz IPlugin e implementa todos los métodos de esa interfaz. Así que, en lugar de heredar de la interfaz IPlugin podemos extender de la clase BasePlugin. Si tenemos alguna lógica que necesita ser ejecutada durante nuestro proceso de instalación y desinstalación de plugins y widgets, entonces podemos anular el método "Instalar" y "Desinstalar" de la clase BasePlugin a nuestra clase. Finalmente la clase debería verse así

```cs
public class HelloWorldPlugin: BasePlugin
{
    public override void Install()
    {
        //Logic during installation goes here...

        base.Install();
    }

    public override void Uninstall()
    {
        //Logic during uninstallation goes here...

        base.Uninstall();
    }
}
```

Ahora construye tu proyecto y corre. Navega al panel de administración y en "Configuración" hay un menú de "Plugins locales", haz clic en ese menú. Aquí verás todos los plugins listados que están presentes en nuestro directorio `Nop.Web/Plugins`. Allí verás tu nuevo plugin creado. Si no lo ve, haga clic en el botón "Reload list of plugins" (Recargar lista de plugins), después reiniciará su aplicación y mostrará todos los plugins disponibles. Ahora deberías ver tu plugin listado en esa lista. Haz clic en el botón verde de instalación presente en la fila de plugins.

![image5](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image5.png)

Ahora, después de hacer clic en el botón de instalación, haga clic en el botón "Reiniciar la aplicación para aplicar los cambios". Esto reiniciará tu aplicación e instalará tu plugin. Después de que la instalación se complete, verás un botón de "Configurar" y "Editar" y otro de "Desinstalar" como este.

![image6](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image6.png) Ahora tu plugin está instalado. Pero el botón "Configurar" no funcionará, ya que no tenemos ninguna página de configuración en nuestro plugin.

## Crear un widget para mostrar algo de UI en nuestro sitio público

Como se mencionó anteriormente, Widget es igual que el plugin pero con características adicionales. Así que podemos usar este mismo proyecto de plugin para convertirlo en widget y renderizar alguna interfaz de usuario a nuestro sitio público. Así que veamos cómo podemos extender este plugin para crear un widget.

Primero necesitamos crear un ViewComponent. Crear un directorio "Componentes" en la raíz del proyecto y crear una clase ViewComponent. Necesitamos extender de esta clase desde la clase base `NopViewComponent`.

```cs
[ViewComponent(Name = "HelloWorldWidget")]
public class ExampleWidgetViewComponent: NopViewComponent
{
    public IViewComponentResult Invoke(string widgetZone)
    {
        return Content("Hello World");
    }
}
```

Ahora vamos a la clase uno que se extiende desde "BasePlugin" que hemos creado previamente, e inherente a la interfaz de IWidgetPlugin. Esta interfaz tiene dos declaraciones de función "GetWidgetZones" y "GetWidgetViewComponentName" que necesitamos implementar en nuestra clase.

```cs
public class HelloWorldPlugin: BasePlugin, IWidgetPlugin
{
    /// <summary>
    /// Gets a value indicating whether to hide this plugin on the widget list page in the admin area
    /// </summary>
    public bool HideInWidgetList => false;

    /// <summary>
    /// Gets widget zones where this widget should be rendered
    /// </summary>
    /// <returns>Widget zones</returns>
    public string GetWidgetViewComponentName(string widgetZone)
    {
        return "HelloWorldWidget";
    }

    /// <summary>
    /// Gets a name of a view component for displaying widget
    /// </summary>
    /// <param name="widgetZone">Name of the widget zone</param>
    /// <returns>View component name</returns>
    public IList<string> GetWidgetZones()
    {
        return new List<string> { "home_page_before_categories" };
    }

    public override void Install()
    {
        //Logic during installation goes here...

        base.Install();
    }

    public override void Uninstall()
    {
        //Logic during uninstallation goes here...

        base.Uninstall();
    }
}
```

Now if you build your project and navigate to admin panel and go to Configuration => Widgets. You will see your widget listed.

![image7](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image7.png)

Aquí puede notar que este widget no tiene el botón "Configurar". Esto se debe a que no creamos un archivo de vista de configuración para este widget y no anulamos el método "GetConfigurationPageUrl" de la clase BasePlugin. Como ya hemos instalado nuestro plugin no tenemos que volver a instalarlo, pero aquí podéis ver que el widget no está activo ahora mismo. Podemos activarlo pulsando el botón de edición.

![image8](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image8.png)

Ahora, después de poner el widget en activo, nuestro widget debería funcionar como se esperaba. Si vamos a nuestra página de inicio antes de la categoría debemos ver el mensaje "Hola Mundo" como se muestra en la imagen resaltada en amarillo.

![image9](_static/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin/image9.png)
