---
title: Description of the web.config file in project
uid: es/developer/tutorials/description-of-the-web-config-file-in-project
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Descripción del archivo web.config en el proyecto

## ¿Qué es el archivo web.config?

El archivo web.config es un archivo de configuración basado en xml que se utiliza en una aplicación basada en ASP.NET para administrar varias configuraciones relacionadas con la configuración de nuestro sitio web. De esta forma podemos separar la lógica de nuestra aplicación de la lógica de configuración. Y el principal beneficio de esto es que, si queremos cambiar algunos ajustes de configuración, entonces no necesitamos reiniciar nuestra aplicación para aplicar nuevos cambios, ASP.NET detecta automáticamente los cambios y los aplica a la aplicación ASP.NET en ejecución.

El marco ASP.NET utiliza un sistema de configuración jerárquica. Puede colocar un archivo Web.Config en cualquier subdirectorio de una aplicación. Luego, el archivo se aplica a cualquier página ubicada en el mismo directorio o subdirectorios.

## web.config para nopCommerce

nopCommerce usa web.config en el proyecto `Nop.Web` que se puede encontrar dentro del directorio de presentación. En la raíz del directorio del proyecto, puede ver un archivo web.config. Si su solución es una instalación nueva de nopCommerce, entonces el contenido de ese archivo se parece a estov.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.webServer>
    <modules>
        <!-- Remove WebDAV module so that we can make DELETE requests -->
        <remove name="WebDAVModule" />
    </modules>
    <handlers>
        <!-- Remove WebDAV module so that we can make DELETE requests -->
        <remove name="WebDAV" />
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <!-- When deploying on Azure, make sure that "dotnet" is installed and the path to it is registered in the PATH environment variable or specify the full path to it -->
    <aspNetCore requestTimeout="23:00:00" processPath="%LAUNCHER_PATH%" arguments="%LAUNCHER_ARGS%" forwardWindowsAuthToken="false" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" startupTimeLimit="3600">
        <environmentVariables />
    </aspNetCore>
    <httpProtocol>
        <customHeaders>
        <remove name="X-Powered-By" />
        <!-- Protects against XSS injections. ref.: https://www.veracode.com/blog/2014/03/guidelines-for-setting-security-headers/ -->
        <add name="X-XSS-Protection" value="1; mode=block" />
        <!-- Protects against Clickjacking attacks. ref.: http://stackoverflow.com/a/22105445/1233379 -->
        <add name="X-Frame-Options" value="SAMEORIGIN" />
        <!-- Protects against MIME-type confusion attack. ref.: https://www.veracode.com/blog/2014/03/guidelines-for-setting-security-headers/ -->
        <add name="X-Content-Type-Options" value="nosniff" />
        <!-- Protects against Clickjacking attacks. ref.: https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet -->
        <add name="Strict-Transport-Security" value="max-age=31536000; includeSubDomains" />
        <!-- CSP modern XSS directive-based defence, used since 2014. ref.: http://content-security-policy.com/ -->
        <add name="Content-Security-Policy" value="default-src 'self'; connect-src *; font-src *; frame-src *; img-src * data:; media-src *; object-src *; script-src * 'unsafe-inline' 'unsafe-eval'; style-src * 'unsafe-inline';" />
        <!-- Prevents from leaking referrer data over insecure connections. ref.: https://scotthelme.co.uk/a-new-security-header-referrer-policy/ -->
        <add name="Referrer-Policy" value="strict-origin" />
        <!--Feature-Policy is a new header that allows a site to control which features and APIs can be used in the browser. ref.: https://wicg.github.io/feature-policy/ -->
        <add name="Feature-Policy" value="accelerometer 'none'; camera 'none'; geolocation 'none'; gyroscope 'none'; magnetometer 'none'; microphone 'none'; payment *; usb 'none'" />
        </customHeaders>
    </httpProtocol>
    </system.webServer>
</configuration>
```

```xml
<configuration>
    ...
</configuration>
```

Todas las reglas de configuración van dentro "`<configuration>`" elemento.

```xml
<system.webServer>
    ...
</system.webServer>
```

El elemento `<system.webServer>` especifica el elemento raíz para muchos de los parámetros de configuración de nivel de sitio y de aplicación para IIS, y contiene elementos de configuración que definen los parámetros utilizados por el motor y los módulos del servidor web.

```xml
<modules>
    <!-- Remove WebDAV module so that we can make DELETE requests -->
    <remove name="WebDAVModule" />
</modules>
```

El elemento `<modules>` define los módulos de código nativo y los módulos de código administrado que están registrados para una aplicación. Normalmente usamos módulos para implementar funciones personalizadas.

el `<modules>` elemento contiene una colección de `<add>`, `<remove>` y`<clear>` elementos.

Aquí nopCommerce está usando `<remove>`elemento para eliminar módulos WebDAVModule de la aplicación.

```xml
<handlers>
    <!-- Remove WebDAV module so that we can make DELETE requests -->
    <remove name="WebDAV" />
    <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
</handlers>
```

Los controladores son componentes de IIS de Internet que están configurados para procesar solicitudes de contenido específico, normalmente para generar una respuesta para el recurso de solicitud. Por ejemplo, una página web ASP.NET es un tipo de controlador. Puede utilizar controladores para procesar solicitudes a cualquier recurso que necesite devolver información a los usuarios que no sea un archivo estático.

El elemento `<handlers>` contiene una colección de elementos `<add>`, `<remove>` y `<clear>`, cada uno de los cuales define un mapeo de manejadores para la aplicación. El elemento `<add>` agrega un manejador a la colección de manejadores, el elemento `<remove>` elimina una referencia de manejador de la colección de manejadores y el elemento `<clear>` elimina todas las referencias de manejadores de la colección de manejadores. Aquí, en el código anterior, se elimina el controlador "WebDAV" y se agrega el controlador para el módulo "AspNetCoreModele".

```xml
<aspNetCore requestTimeout="23:00:00" processPath="%LAUNCHER_PATH%" arguments="%LAUNCHER_ARGS%" forwardWindowsAuthToken="false" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" startupTimeLimit="3600">
    <environmentVariables />
</aspNetCore>
```

```xml
<httpProtocol>
    <customHeaders>
        <remove name="X-Powered-By" />
        <!-- Protects against XSS injections. ref.: https://www.veracode.com/blog/2014/03/guidelines-for-setting-security-headers/ -->
        <add name="X-XSS-Protection" value="1; mode=block" />
        <!-- Protects against Clickjacking attacks. ref.: http://stackoverflow.com/a/22105445/1233379 -->
        <add name="X-Frame-Options" value="SAMEORIGIN" />
        <!-- Protects against MIME-type confusion attack. ref.: https://www.veracode.com/blog/2014/03/guidelines-for-setting-security-headers/ -->
        <add name="X-Content-Type-Options" value="nosniff" />
        <!-- Protects against Clickjacking attacks. ref.: https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet -->
        <add name="Strict-Transport-Security" value="max-age=31536000; includeSubDomains" />
        <!-- CSP modern XSS directive-based defence, used since 2014. ref.: http://content-security-policy.com/ -->
        <add name="Content-Security-Policy" value="default-src 'self'; connect-src *; font-src *; frame-src *; img-src * data:; media-src *; object-src *; script-src * 'unsafe-inline' 'unsafe-eval'; style-src * 'unsafe-inline';" />
        <!-- Prevents from leaking referrer data over insecure connections. ref.: https://scotthelme.co.uk/a-new-security-header-referrer-policy/ -->
        <add name="Referrer-Policy" value="strict-origin" />
        <!--Feature-Policy is a new header that allows a site to control which features and APIs can be used in the browser. ref.: https://wicg.github.io/feature-policy/ -->
        <add name="Feature-Policy" value="accelerometer 'none'; camera 'none'; geolocation 'none'; gyroscope 'none'; magnetometer 'none'; microphone 'none'; payment *; usb 'none'" />
    </customHeaders>
</httpProtocol>
```

El elemento `<customHeaders>` del elemento `<httpProtocol>` especifica los encabezados HTTP personalizados que IIS devolverá en las respuestas HTTP del servidor web.

Los encabezados HTTP son pares de nombre y valor que se devuelven en las respuestas de un servidor web. Los encabezados de respuesta personalizados se envían al cliente junto con el encabezado HTTP predeterminado. A diferencia de los encabezados de respuesta de redireccionamiento, que se devuelven en las respuestas solo cuando se produce el redireccionamiento, los encabezados de respuesta personalizados se devuelven en cada respuesta.

## Configurar las reglas de redireccionamiento en IIS

Podemos agregar otras configuraciones adicionales a las configuraciones anteriores. Aquí veremos cómo configurar las reglas de redireccionamiento en IIS.

Una regla de redireccionamiento permite que más de una URL apunte a una sola página web. Puede haber varias razones por las que desee redirigir la solicitud de un servidor a otro. Por ejemplo, puede ser que se haya cambiado el nombre de su empresa y es posible que desee registrar un nuevo dominio para su empresa y mover su sitio web a un nuevo dominio, por lo que en ese caso es posible que desee redirigir todas las solicitudes de su antiguo dominio al nuevo dominio.

Para que nuestro sitio web pueda usar reglas de redireccionamiento, necesitamos instalar el módulo de reescritura de URL, que es una extensión de IIS.

Para fines de demostración, digamos que tenemos que redirigir la solicitud a nuestro sitio anterior a nuestro nuevo sitio, para eso necesitamos escribir las siguientes reglas en nuestro archivo web.config.

```xml
<rewrite>
  <rules>
     <rule name="[RULE NAME]" stopProcessing="true">
     <match url="(.*)" />
     <conditions logicalGrouping="MatchAny" trackAllCaptures="false">
        <add input="{HTTP_HOST}{REQUEST_URI}" pattern="[OLD URL]" />
     </conditions>
     <action type="Redirect" url="http://[NEW URL]/{R:1}" redirectType="Permanent"/>
     </rule>
  </rules>
</rewrite>
```

> [!NOTE]
>
> Al usar esta regla, podemos redirigir todas las páginas de un nombre de dominio antiguo a la misma página en un nombre de dominio nuevo.

Aquí necesitamos reemplazar [NOMBRE DE LA REGLA], [URL ANTIGUA] y [URL NUEVA] con la información apropiada.

* [NOMBRE DE LA REGLA] puede ser cualquier cosa que describa lo que hace esta regla
* [OLD URL] es la URL antigua desde la que desea redirigir.
* [NUEVA URL] es la nueva URL a la que desea redirigir.

```xml
<match url="(.*)" />
```

El elemento anterior hace referencia a que esta regla coincidirá con todas las cadenas de URL.

```xml
<add input="{HTTP_HOST}{REQUEST_URI}" pattern="[OLD URL]" />
```

El elemento anterior agrega una condición a la regla que recupera el host y solicita el valor del encabezado uri leyendo la variable del servidor HTTP_HOST y REQUEST_URI y la compara con el patrón con el valor proporcionado para [OLD URL].

```xml
<action type="Redirect" url="http://[NEW URL]/{R:1}" redirectType="Permanent"/>
```

Este elemento redirige la URL anterior coincidente a la nueva URL.
