---
title: System requirements for developing
uid: en/developer/tutorials/system-requirements-for-developing
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

> [!NOTE]
>
> Para obtener más información sobre la compatibilidad de los navegadores, visite [Supported OS versions](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md)

## 1. Navegadores soportados

* Microsoft Internet Explorer 9 y superior (IE6 e IE7 eran compatibles en las versiones anteriores a la 3.60, IE8 era compatible en las versiones anteriores a la 4.10)
* Mozilla Firefox 2.0 y superior
* Google Chrome 1.x
* Apple Safari 2.x

## 2. Herramientas necesarias para el desarrollo

Como está basado en el marco ASP.NET de Microsoft, necesitamos instalar algunas herramientas antes de empezar a desarrollar en nopCommerce.

### \.NET Core 3.1 runtime & .NET Core SDK

Ya que nopCommerce 4.30 está basado en el marco de .NET Core 3.1. Necesitamos instalar [.NET Core 3.1 runtime](https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer) y [.NET Core SDK](https://dotnet.microsoft.com/download/dotnet-core/thank-you/sdk-3.1.201-windows-x64-installer) antes de empezar el desarrollo en nopCommerce.

### Visual Studio 2019 o superior / Código de Visual Studio

Como sabemos, nopCommerce se basa en el 'ASP.NET framework' de Microsoft y Visual Studio IDE es el mejor para desarrollar aplicaciones basadas en Dot Net. Ya que el núcleo de .NET es independiente de la plataforma, podemos desarrollar y desplegar aplicaciones basadas en .Net en cualquier plataforma, pero Visual Studio no está disponible en otras plataformas que no sean Windows. Así que podemos usar el código de Visual Studio como la alternativa de Visual Studio para desarrollar en Windows así como en otra plataforma.

### Microsoft SQL Server 2012 o superior / MySql Server 5.7 o superior

A partir de la versión 4.30 nopCommerce utiliza Linq2DB como marco de trabajo ORM. Linq2DB es un mapeador objeto-relacional (ORM) que permite a los desarrolladores de .NET trabajar con una base de datos usando objetos .NET. Puede mapear objetos .Net a varios números de proveedores de bases de datos. Y puede elegir entre MS SQL Server y MySql server.

### Servicio de Información de Internet (IIS) 7.0 o superior

Para alojar un proyecto o aplicación de nopCommerce podemos usar IIS. Que es la tecnología de Microsoft utilizada para alojar aplicaciones web de Microsoft en Windows. Pero no estás limitado para alojar tu nopCommerce en windows sólo puedes alojar nopCommerce en Linux y MacOS también. Como sabrán, IIS no está soportada en otra plataforma que no sea Windows. Por lo tanto, puedes usar otras herramientas como Apache o Nginx para alojar tu aplicación en un servidor Linux.
