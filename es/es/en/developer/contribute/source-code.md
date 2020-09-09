---
title: Working with source code and contributions
uid: en/developer/contribute/source-code
author: git.AndreiMaz
contributors: git.RomanovM, git.exileDev
---

# Trabajar con código fuente y contribuciones

# Desproteger el código fuente

nopCommerce administra un repositorio en GitHub ([https://github.com/nopSolutions/nopCommerce](https://github.com/nopSolutions/nopCommerce)). Así que siempre se puede echar un vistazo al último código fuente! Git SCM (Administración de código fuente) acceso es público y le permite buscar en tiempo real la última versión de nopCommerce! Le permite seguir los desarrollos y mejoras diarias de nopCommerce. Obtenga los últimos parches, correcciones sin esperar a la próxima versión. Si no estás familiarizado con Git, hay una buena y gratuita documentación [aquíhere](https://git-scm.com/docshttps://git-scm.com/docs). También encontrar más información sobre el soporte de GitHub [aquí](https://opensource.guide/how-to-contribute/). Tenga en cuenta que estas versiones no deben utilizarse en un entorno de producción. No garantizamos que ninguna de las funciones o códigos que se encuentran en nuestro SCM (Source Code Management) estará disponible en nuestras versiones oficiales. La mejor manera de obtener el código fuente es clonar el repositorio. Git viene con herramientas de gui de usuario integradas para comprometer (git-gui) y navegar (gitk), pero hay varias herramientas de terceros para los usuarios que buscan experiencia específica de la plataforma. Por favor, en [https://git-scm.com/downloads/guis](https://git-scm.com/downloads/guis) (utilizamos [SourceTree](https://www.sourcetreeapp.com/)).

# Descripciones y nomenclatura de sucursales

Recientemente comenzamos a utilizar el modelo de ramificación de Vincent Driessen (visto aquí: [http://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)) incluyendo el uso de ramas de características, una rama de desarrollo (para la integración) y una rama maestra (para la publicación / producción). Anteriormente teníamos "maestro" rama solamente (hasta enero de 2016)

* Rama de producción: maestro
* Rama de desarrollo: desarrollo
* Características y ramas de emisión: Debe comenzar con "característica" o "problema". Debe ir seguido de un ID de problema (según nuestra lista de problemas de Github) y algún nombre descriptivo (por ejemplo, "multistore"). Por último, debería parecerse a "feature-34-multistore" o "issue-35-paypal-redirection-bug"
* Liberar ramas: Debe comenzar con "liberación". Debe ir seguido del número de versión (por ejemplo, "3.00"). Por último, debería parecerse a "release-3.00"

# Bifurcar y enviar solicitudes de extracción

Si desea contribuir con algún código fuente al núcleo de nopCommerce (corrección de problemas o alguna característica nueva), entonces debe seguir el siguiente enfoque. Aquí está una breve lista de pasos para contribuir:

* En primer lugar, tienes que crear un tenedor. Encontrará más información sobre la bifurcación del repositorio en GitHub en [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/).
* Clonarlo localmente.
* Crear una nueva rama de "desarrollar". Por favor, cree siempre una nueva sucursal para cada contribución. Debe crearlo únicamente a partir de nuestra rama de "desarrollo". No utilice "maestro".
* Escriba el código y vuelva a su bifurcación de GitHub.
* Crear solicitud de extracción. Por favor, lea más sobre esto en [https://help.github.com/articles/using-pull-requests/](https://help.github.com/articles/using-pull-requests/). Y por favor, siempre sincronice con nuestro repositorio antes de hacerlo.


