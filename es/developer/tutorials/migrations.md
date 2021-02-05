---
title: How do migrations work?
uid: es/developer/tutorials/migrations
author: git.AndreiMaz
contributors: git.skoshelev
---
# ¿Cómo funcionan las migraciones?

## Breve descripción de los cambios realizados en el enfoque para trabajar con la base de datos

El trabajo con la base de datos fue reelaborado significativamente en la versión 4.30 de nopCommerce. El primer cambio que se pudo notar es un completo rechazo de las propiedades de navegación. Podemos pensar y discutir sobre la utilidad de este enfoque, pero definitivamente tiene un par de puntos positivos:

1. Simplifique la comprensión y el mantenimiento del código.
    > [!NOTE]
    > Durante la refactorización del código, encontramos y corregimos varias inexactitudes que afectan tanto al rendimiento como a la funcionalidad.
1. Control total sobre las consultas y el momento de su ejecución (lo que afecta positivamente el desempeño de toda la solución).
1. Posibilidad de simplificar el proceso de migración a cualquier marco de base de datos (lo más importante).

Dado que nopCommerce cambió completamente a .Net Core (versión 4.10) y se convirtió en una solución multiplataforma, el soporte de varias bases de datos se convierte en un tema cada vez más importante. El equipo de nopCommerce ha realizado una investigación y un análisis considerables y decidió abandonar el uso del Entity Framework Core estándar. Al mismo tiempo, decidimos no trabajar con la base de datos a través de consultas LINQ utilizando el enfoque OOP (que es el enfoque más común utilizado por los desarrolladores de C #). La elección final recayó en un grupo de Linq2DB y FluentMigrator. A continuación, describiré el papel de cada uno de estos marcos en detalle.

## Linq2DB

> [!NOTE]
> A partir de la versión 4.30, nopCommerce usa Linq2DB como marco ORM. Linq2DB es un mapeador relacional de objetos (ORM) que permite a los desarrolladores .NET trabajar con una base de datos utilizando objetos .NET. Puede asignar objetos .Net a varios proveedores de bases de datos.

En nopCommerce, Linq2DB se utiliza como nivel de acceso a la base de datos. Actualmente, nopCommerce admite dos de las bases de datos más populares: MS SQL Server y MySQL Server. Si analizamos el código, podemos ver fácilmente que cada base de datos es compatible con su propia clase que implementa la interfaz INopDataProvider. Pero si no planea crear su propio proveedor de acceso a la base de datos, puede ignorar los detalles de implementación. Para la mayoría de las tareas de desarrollo, será suficiente comprender solo algunos puntos:

1. Necesita un objeto correspondiente a la tabla en la base de datos (clase POCO).
1. Todo el trabajo con datos de tablas se realiza a través de la interfaz IRepository `<TEntity>`. Ni siquiera es necesario que se ocupe de su colocación en el IoC, ya que se registra mediante una llamada al método de fábrica correspondiente.
1. Necesita controlar la creación de la tabla en la base de datos.

Y para resolver el último problema, tenemos que lidiar con el segundo marco del paquete, es decir, con FluentMigrator.

## FluentMigrator

> [!NOTE]
> Fluent Migrator es un marco de migración para .NET muy parecido a Ruby on Rails Migrations. *Las migraciones* son una forma estructurada de alterar el esquema de su base de datos y son una alternativa a la creación de muchos scripts SQL que deben ser ejecutados manualmente por cada desarrollador involucrado. Las migraciones resuelven el problema de desarrollar un esquema de base de datos para múltiples bases de datos (por ejemplo, base de datos local del desarrollador, base de datos de prueba y base de datos de producción). Los cambios en el esquema de la base de datos se describen en clases escritas en C #. Estas clases se pueden registrar en un sistema de control de versiones.

El plan detallado para agregar sus entidades se describe en el siguiente artículo: [Complemento con acceso a datos](xref:es/developer/plugins/how-to-write-plugin-4.30). Por lo tanto, nos quedaremos solo en puntos teóricos generales:

1. Las migraciones se admiten a nivel del código nopCommerce en sí.
1. Puede crear cualquier migración heredada de la clase abstracta **MigrationBase**.
1. Para simplificar el control de versiones para las migraciones, agregamos el atributo **NopMigrationAttribute** heredado de **MigrationAttribute** al código. Ahora puede simplemente especificar la fecha y la hora en que se creó la migración en lugar del número largo habitual.
1. También agregamos el atributo **SkipMigrationOnUpdateAttribute** que indica si se debe omitir una migración durante el proceso de actualización.
1. Puede crear una tabla en la base de datos de dos formas:
    * Utilice el método **Create.Table** en el método **Up** de su clase de migración y especifique todos los detalles utilizando los métodos de extensión.
    * Use el método **IMigrationManager.BuildTable \ <T \>** en el método **Up** de su clase de migración y especifique todos los detalles, si es necesario, usando la implementación de **IEntityBuilder** y **INameCompatibility** interfaces (en nopCommerce usamos este enfoque).