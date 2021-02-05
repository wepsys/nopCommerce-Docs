---
title: System requirements for developing
uid: es/developer/tutorials/system-requirements-for-developing
author: nop.sea
contributors: git.RomanovM, git.DmitriyKulagin
---

# Requisitos del sistema para desarrollar

## Sistema operativo

* Windows

| OS                | Version       |
| ----------------- | ------------- |
| Windows Client    | 7 SP1+, 8.1   |
| Windows 10 Client | Version 1607+ |
| Windows Server    | 2012 R2+      |

* Linux

| OS                           | Version             |
| ---------------------------- | ------------------- |
| Red Hat Enterprise Linux     | 6+                  |
| CentOS, Oracle Linux         | 7+                  |
| Fedora                       | 30+                 |
| Debian                       | 9+                  |
| Ubuntu                       | 18.04, 19.10, 20.04 |
| Linux Mint                   | 18+                 |
| OpenSUSE                     | 15+                 |
| SUSE Enterprise Linux (SLES) | 12 SP2+             |
| Alpine Linux                 | 3.10+               |

* MacOS

| OS       | Version |
| -------- | ------- |
| Mac OS X | 10.13+  |

> [!NOTA]
>
> Para obtener más información sobre el soporte del navegador, visite [Versiones compatibles del sistema operativo](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md)

## 1. Navegadores compatibles

* Microsoft Internet Explorer 9 y superior (IE6 e IE7 eran compatibles con versiones anteriores a 3.60, IE8 era compatible con versiones anteriores a 4.10)
* Mozilla Firefox 2.0 y superior
* Google Chrome 1.x
* Apple Safari 2.x

## 2. Herramientas necesarias para el desarrollo

Dado que se basa en el marco de ASP.NET de Microsoft, necesitamos instalar algunas herramientas antes de empezar a desarrollar en la parte superior de nopCommerce.

# Tiempo de ejecución de .NET Core 3.1 y SDK de .NET Core

Dado que nopCommerce 4.30 se basa en el marco de .NET Core 3.1. Necesitamos instalar [.NET Core 3.1 runtime](https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer)y [.NET Core SDK](https://dotnet.microsoft.com/download/dotnet-core/thank-you/sdk-3.1.201-windows-x64-installer) antes de comenzar el desarrolloen nopCommerce.

# Visual Studio 2019 o Superior/Visual Studio Code

Como sabemos nopCommerce se basa en 'Microsoft's ASP.NET framework' y Visual Studio IDE es mejor para el desarrollo de aplicaciones basadas en Dot Net. Dado que .NET Core es independiente de la plataforma, por lo que podemos desarrollar e implementar aplicaciones basadas en .Net en cualquier plataforma, pero visual studio no está disponible en otras plataformas que no sean windows. Por lo tanto, podemos usar Visual Studio Code como alternativa de Visual Studio para desarrollar en Windows, así como en otra plataforma.

# Microsoft SQL Server 2012 o Superior/MySql Server 5.7 o superior

Iniciado a partir de la versión 4.30 nopCommerce utiliza Linq2DB como un marco ORM. Linq2DB es un asignador relacional de objetos (ORM) que permite a los desarrolladores de .NET trabajar con una base de datos mediante objetos .NET. Puede asignar objetos .Net a varios números de proveedores de bases de datos. Y puede elegir entre MS SQL Server y el servidor MySql.

# Servicio de Información de Internet (IIS) 7.0 o superior

Para alojar aplicación/proyecto nopCommerce podemos usar IIS. Que es la tecnología de Microsoft utilizada para hospedar aplicaciones basadas en web de Microsoft en Windows. Pero usted no está limitado para alojar su nopCommerce en Windows sólo usted puede alojar nopCommerce en Linux y MacOS también. Como puede saber que IIS no se admite en otra plataforma, a continuación, Windows. Por lo tanto, puede utilizar otras herramientas como Apache o Nginx para alojar su aplicación en el servidor Linux.
