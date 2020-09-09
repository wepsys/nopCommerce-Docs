---
title: nopCommerce Data Access Layer
uid: en/developer/tutorials/data-access-layer
author: git.AndreiMaz
contributors: git.exileDev
---

# nopCommerce Data Access Layer (Capa de acceso a datos nopCommerce)

El proyecto Nop.Data contiene un conjunto de clases y funciones para leer y escribir en una base de datos u otro almacén de datos. La biblioteca Nop.Data ayuda a separar la lógica de acceso a datos de sus objetos comerciales. nopCommerce utiliza el enfoque Linq2DB Code-First. Code-First permite a un desarrollador definir entidades en el código fuente (todas las entidades centrales se definen en el proyecto Nop.Core) y luego usar Linq2DB y FluentMigrator para generar la base de datos a partir de las clases C #. Por eso se llama Code-First. Luego puede consultar sus objetos usando LINQ, que se traduce a SQL detrás de escena y se ejecuta en la base de datos. NopCommerce usa [API fluida](https://fluentmigrator.github.io/articles/technical/fluent-api-create.html) para personalizar completamente el mapeo de persistencia.
