---
title: A guide to expanding the functionality of the basic functions of nopCommerce through a plugin
uid: en/developer/tutorials/guide-to-expanding-the-functionality-of-the-basic-functions-of-nop-commerce-through-a-plugin
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Una guía para expandir la funcionalidad de las funciones básicas de nopCommerce a través de un complemento

## Visión general

nopCommerce utiliza el sistema de complementos para ampliar la funcionalidad del panel de administración de nopCommerce y utiliza el sistema de widgets para ampliar la funcionalidad del sitio web. Los complementos y widgets son un conjunto de programas o componentes independientes que se pueden agregar a un sistema existente para ampliar alguna funcionalidad específica y también se pueden eliminar del sistema sin afectar el sistema principal durante el proceso. Entonces, al usar el concepto de complemento y widgets, podemos agregar más funcionalidad a nuestro sistema y podemos construirlos sin alterar o editar el código fuente central de la solución nopCommerce. Lo que nos permite actualizar o degradar nuestra solución nopCommerce a la última versión o una versión anterior según lo deseemos sin tener que volver a escribir el complemento y los widgets que ya hemos creado.

## Diferencia entre complemento y widget

Como sabemos, tanto el complemento como el widget sirven para ampliar la funcionalidad de la solución nopCommerce. Bueno, entonces puedes preguntar "cuál es la diferencia entre ellos". En última instancia, en nopCommerce puede pensar en el widget como un complemento pero con una función adicional. Para crear un widget, el proceso es básicamente el mismo que el de crear un complemento, pero al usar el widget podemos mostrar alguna IU (interfaz de usuario) al sitio web público de nopCommerce en algunas áreas específicas predefinidas por nopCommerce que se conocen como zonas de widgets. Lo que no podemos lograr solo a través de un complemento. Puede pensar que el widget es un superconjunto de complementos.

Creo que tienes más claro qué son los widgets y complementos, cuándo se pueden usar y cuáles son los beneficios de usarlos. Entonces, ahora vamos a crear un widget simple que muestre el mensaje "Hola mundo" en el sitio público, para comprender cómo crear un widget en nopCommerce.

## Inicializar proyecto de complemento

### Paso 1: Crea un nuevo proyecto

Vaya al sitio web oficial de nopCommerce y descargue el último código fuente de nopCommerce. Dado que en este momento la última versión es 4.2, esta documentación está escrita de acuerdo con v4.2. Abra su solución nopCommerce en su IDE favorito (se recomienda Visual Studio). Allí verá un montón de carpetas. Si desea saber todo sobre la estructura de carpetas, es posible que desee visitar la documentación de nopCommerce. En el techo de la solución verá una carpeta "Complementos", expanda esa carpeta y verá una lista de proyectos de complementos enviados con nopCommerce por defecto.

![image1](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-mediante-un-complemento/image1.png)

Para crear un nuevo proyecto de widget, haga clic con el botón derecho en la carpeta "Complementos": Agregar => Nuevo proyecto. Después de eso, aparecerá la ventana Agregar nuevo proyecto.

![image2](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-a-través-de-un-complemento/image2.png)

De la lista de la izquierda del tipo de proyecto, seleccione ".NetCore" y elija la plantilla de proyecto "Biblioteca de clases". nopCommerce sigue una conversión de nombres estándar, que puede obtener más información en la documentación de nopCommerce. He elegido "Nop.Plugin.Widget.HelloWorld" como el nombre de mi proyecto siguiendo la conversión de nombres de nopCommerce. Y la ubicación debe estar dentro del directorio "/ source / Plugins". Ahora haga clic en "Aceptar". Esto debería crear un nuevo proyecto dentro del directorio de complementos. Y puede ver en su solución así:

![image3](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-a-través-de-un-complemento/image3.png)

### Paso 2: Configura tu nuevo proyecto para usarlo como Widget

Necesitamos configurar un par de cosas en nuestro proyecto para que se use como complemento o widget.

Después de crear su proyecto, abra con éxito su archivo .csproj, para eso, haga clic derecho en su proyecto y haga clic en el menú {Your_Project_Name.csproj} del menú contextual y reemplace su contenido con el siguiente código.

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

Aquí reemplace {Plugin_Output_Directory} por el nombre de su proyecto, en mi caso "Widget.HelloWorld".

Lo que esto hará es copiar todos los archivos dll relacionados con este proyecto en el `Nop.Web/Plugin/{Plugin_Output_Directory}`, porque el directorio Plugin dentro de `Nop.Web` es la ubicación donde nopCommerce busca desde plugins y widgets para mostrar en Lista de complementos o widgets en el panel de administración.

### Paso 3: Crea un archivo Plugin.json

Este archivo es necesario para todos los complementos o widgets que creamos en nopCommerce. Este archivo contiene metainformación sobre nuestro complemento que describe nuestro complemento. Contiene información como el nombre de nuestro complemento, la versión de nopCommerce para la que está diseñado o diseñado, una descripción sobre nuestro complemento, la versión de nuestro complemento, etc. Después de crear el archivo "Plugin.json", copie este contenido dentro de su archivo y modifíquelo de acuerdo con sus requisitos..

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

NopCommerce usa este archivo al incluir nuestro complemento/widget en la lista de complementos en el panel de administración y para identificar nuestro complemento de manera única entre todos los complementos instalados y desinstalados en toda la aplicación. Entonces, para que nopCommerce pueda leer este archivo, necesitamos copiar este archivo en su directorio de salida mientras construimos el proyecto. Para hacerlo, haga clic derecho en el archivo Plugin.json y haga clic en propiedad. En Propiedad, establezca el valor de "Copiar en el directorio de salida" a "copiar si es más reciente"

![image4](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-mediante-un-complemento/image4.png)

### Paso 4: Crea una clase que se extienda desde BasePlugin Class

En realidad, necesitamos tener una clase inherente a la interfaz de IPlugin para que nopCommerce trate nuestro proyecto como un complemento. Pero nopCommerce ya tiene una clase "BasePlugin" que hereda de la interfaz IPlugin e implementa todos los métodos de esa interfaz. Entonces, en lugar de heredar de la interfaz IPlugin, podemos extendernos desde la clase BasePlugin. Si tenemos alguna lógica que debe ejecutarse durante nuestro proceso de instalación y desinstalación de complementos / widgets, entonces podemos anular el método "Instalar" y "Desinstalar" de la clase BasePlugin a nuestra clase. Finalmente, la clase debería verse así

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

Ahora cree su proyecto y ejecútelo. Navegue al panel de administración y en "Configuración" hay un menú de "Complementos locales", haga clic en ese menú. Aquí verá todos los complementos enumerados que están presentes en el directorio `Nop.Web/ Plugins`. Allí verá su complemento recién creado. Si no lo ve, haga clic en el botón "Volver a cargar la lista de complementos", luego reiniciará su aplicación y enumerará todos los complementos disponibles. Ahora debería ver su complemento en esa lista. Haga clic en el botón de instalación verde presente en la fila de complementos.

![image5] (_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-a-través-de-un-complemento/image5.png)

Ahora, después de hacer clic en el botón de instalación, haga clic en el botón "Reiniciar su aplicación para aplicar los cambios". Reiniciará su aplicación e instalará su complemento. Una vez completada la instalación, verá un botón "Configurar" y "Editar" y un "botón Desinstalar" como este.

![image6] (_static/guide-to-expand-the-functions-of-the-basic-functions-of-nop-commerce-through-a-plugin/image6.png) Ahora su complemento está instalado. Pero el botón "Configurar" no funcionará, ya que no tenemos ninguna página de configuración en nuestro complemento.

## Crea un widget para mostrar alguna IU en nuestro sitio público

Como se mencionó anteriormente, el widget es igual que el complemento pero con características adicionales. Entonces, podemos usar este mismo proyecto de complemento para convertirlo en un widget y representar una interfaz de usuario en nuestro sitio público. Así que veamos cómo podemos extender este complemento para crear un widget.

Primero necesitamos crear un ViewComponent. Cree un directorio "Componentes" en la raíz del proyecto y cree una clase ViewComponent. Necesitamos extendernos desde esta clase desde la clase base `NopViewComponent`.

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

Ahora ve a la clase uno que se extiende desde "BasePlugin" que hemos creado previamente, e inherente a la interfaz IWidgetPlugin. Esta interfaz tiene dos declaraciones de función "GetWidgetZones" y "GetWidgetViewComponentName" que necesitamos implementar en nuestra clase.

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

Ahora, si construye su proyecto y navega hasta el panel de administración y vaya a Configuración => Widgets. Verá su widget en la lista.

![image7](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-mediante-un-complemento/image7.png)

Aquí puede notar que este widget no tiene el botón "Configurar". Esto se debe a que no creamos un archivo de vista de configuración para este widget y no anulamos el método "GetConfigurationPageUrl" de la clase BasePlugin. Como ya hemos instalado nuestro complemento, no tenemos que volver a instalarlo, pero aquí puede ver que el widget no está activo en este momento. Podemos activar esto haciendo clic en el botón editar.

![image8](_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-a-través-de-un-complemento/image8.png)

Ahora, después de configurar el widget como activo, nuestro widget debería funcionar como se esperaba. Si vamos a nuestra página de inicio antes de la categoría debemos ver el mensaje "Hola mundo" como se muestra en la imagen resaltada en amarillo.

![image9] (_estática/guía-para-expandir-la-funcionalidad-de-las-funciones-básicas-de-nop-commerce-mediante-un-complemento/image9.png)
