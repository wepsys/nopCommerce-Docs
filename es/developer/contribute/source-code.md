---
title: Working with source code and contributions
uid: es/developer/contribute/source-code
author: git.AndreiMaz
contributors: git.RomanovM, git.exileDev
---

# Trabajar con código fuente y contribuciones

## Comprobando el código fuente

nopCommerce administra un repositorio en GitHub ([https://github.com/nopSolutions/nopCommerce](https://github.com/nopSolutions/nopCommerce)). ¡Así que siempre puedes consultar el código fuente más reciente! El acceso a Git SCM (Source Code Management) es público y le permite obtener en tiempo real la última versión de nopCommerce. Le permite seguir los desarrollos y mejoras diarios de nopCommerce. Obtenga los últimos parches y correcciones sin esperar la próxima versión. Si no está familiarizado con Git, hay una buena documentación gratuita  [aquí](https://git-scm.com/docs). También encontrará más información sobre el soporte de GitHub [aquí](https://opensource.guide/how-to-contribute/). Tenga en cuenta que estas versiones no deben utilizarse en un entorno de producción. No garantizamos que ninguna de las funciones o códigos que se encuentran en nuestro SCM (Gestión de código fuente) estarán disponibles en nuestras versiones oficiales. La mejor forma de obtener el código fuente es clonar el repositorio. Git viene con herramientas GUI integradas para confirmar (git-gui) y navegar (gitk), pero hay varias herramientas de terceros para los usuarios que buscan una experiencia específica de la plataforma. Encuéntrelos en [https://git-scm.com/downloads/guis](https://git-scm.com/downloads/guis) (usamos [SourceTree](https://www.sourcetreeapp.com/)).

## Descripciones y nombres de sucursales

Recientemente comenzamos a usar el modelo de ramificación de Vincent Driessen (visto aquí: [http://nvie.com/posts/a-successful-git-branching-model/]
(https://nvie.com/posts/a-successful-git-branching-model/)) que incluye el uso de ramas de funciones, una rama de desarrollo (para integración) y una rama maestra (para publicación / producción). Anteriormente solo teníamos una rama "maestra" (hasta enero de 2016)

* Rama de producción: maestro
* Rama de desarrollo: desarrollar
* Ramas de características y problemas: debe comenzar con "característica" o "problema". Debe ir seguido del ID del problema (de acuerdo con nuestra lista de problemas de Github) y algún nombre descriptivo (por ejemplo, "multitienda"). Por último, debería verse como "feature-34-multistore" o "issue-35-paypal-redirection-bug"
* Ramas de lanzamiento: debe comenzar con "lanzamiento". Debe ir seguido del número de versión (ejemplo, "3.00"). Finalmente, debería verse como "release-3.00"

## Bifurcar y enviar solicitudes de extracción

Si desea contribuir con algún código fuente al núcleo de nopCommerce (solución de problemas o alguna característica nueva), debe seguir el siguiente enfoque. Aquí hay una breve lista de pasos para contribuir:

* En primer lugar, debes crear una bifurcación. Para obtener más información sobre la bifurcación del repositorio en GitHub, visite [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/).
* Clonarlo localmente.
* Crear una nueva rama desde "desarrollar". Cree siempre una nueva rama para cada contribución. Debe crearlo desde nuestra rama "desarrollar" únicamente. No utilice "maestro".
* Escriba el código y vuelva a enviarlo a su bifurcación de GitHub.
* Crear solicitud de extracción. Lea más sobre esto en [https://help.github.com/articles/using-pull-requests/](https://help.github.com/articles/using-pull-requests/). Y siempre sincronice con nuestro repositorio antes de hacerlo.