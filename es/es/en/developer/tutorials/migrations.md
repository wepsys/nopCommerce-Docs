---
title: How do migrations work?
uid: en/developer/tutorials/migrations
author: git.AndreiMaz
contributors: git.skoshelev
---
# ¿Cómo funcionan las migraciones?

## Breve descripción de los cambios realizados en el enfoque de trabajo con la base de datos

El trabajo con la base de datos fue significativamente reelaborado en la versión 4.30 de nopCommerce. El primer cambio que se pudo notar es un completo rechazo de las propiedades de navegación. Podemos pensar y discutir sobre la utilidad de este enfoque, pero definitivamente tiene un par de puntos positivos:

1. Simplifica la comprensión y el mantenimiento del código.
    > [!NOTE]
    > Durante la refactorización del código, encontramos y corregimos varias inexactitudes que afectaban tanto al rendimiento como a la funcionalidad.
1. Control total sobre las consultas y el momento de su ejecución (lo que afecta positivamente al rendimiento de toda la solución).
1. 2. Posibilidad de simplificar el proceso de migración a cualquier marco de base de datos (lo más importante).

Desde que nopCommerce cambió completamente a .Net Core (versión 4.10) y se convirtió en una solución multiplataforma, el soporte de varias bases de datos se convierte en un tema cada vez más importante. El equipo de nopCommerce ha llevado a cabo una considerable investigación y análisis y ha decidido abandonar el uso del estándar Entity Framework Core. Al mismo tiempo, decidimos no trabajar con la base de datos a través de consultas LINQ utilizando el enfoque OOP (que es el enfoque más común utilizado por los desarrolladores de C#). La elección final recayó en un montón de Linq2DB y FluentMigrator. A continuación, describiré el papel de cada uno de estos marcos en detalle.

## Linq2DB

> [!NOTE]
> A partir de la versión 4.30 nopCommerce utiliza Linq2DB como marco de trabajo ORM. Linq2DB es un mapeador objeto-relacional (ORM) que permite a los desarrolladores de .NET trabajar con una base de datos usando objetos .NET. Puede mapear objetos .Net a varios números de proveedores de bases de datos.

En nopCommerce, Linq2DB se utiliza como un nivel de acceso a la base de datos. Actualmente, nopCommerce soporta dos de las bases de datos más populares: MS SQL Server y MySQL Server. Si analizamos el código, podemos ver fácilmente que cada base de datos es soportada por su propia clase que implementa la interfaz INopDataProvider. Pero si no planea crear su propio proveedor de acceso a la base de datos, puede ignorar los detalles de implementación en absoluto. Para la mayoría de las tareas de desarrollo, la comprensión de sólo unos pocos puntos será suficiente:

1. Necesita un objeto que corresponda a la tabla de la base de datos (clase POCO).
1. Todo el trabajo con los datos de la tabla se lleva a cabo a través de la interfaz del IRepositorio `<TEntidad>`. No es necesario ni siquiera ocuparse de su colocación en la IO, ya que se registra a través de una llamada al método de fábrica apropiado.
1. Necesitas controlar la creación de la tabla en la base de datos.

Y para resolver el último problema, tenemos que ocuparnos del segundo marco del paquete, a saber, con FluentMigrator.

## FluentMigrator

> [!NOTE]
> Fluent Migrator es un marco de migración para .NET muy parecido a Ruby on Rails Migrations. *Las migraciones* son una forma estructurada de alterar el esquema de tu base de datos y son una alternativa a la creación de muchos scripts sql que tienen que ser ejecutados manualmente por cada desarrollador involucrado. Las migraciones resuelven el problema de la evolución del esquema de una base de datos para múltiples bases de datos (por ejemplo, la base de datos local del desarrollador, la base de datos de prueba y la base de datos de producción). Los cambios en el esquema de la base de datos se describen en clases escritas en C#. Estas clases se pueden comprobar en un sistema de control de versiones.

El plan detallado de añadir sus entidades se describe en el siguiente artículo:[Plugin with data access](xref:en/developer/plugins/how-to-write-plugin-4.30). Por lo tanto, nos quedaremos sólo en los puntos teóricos generales:

1. Las migraciones se soportan a nivel del propio código de nopCommerce.
1. Puedes crear cualquier migración heredada de la clase abstracta **MigrationBase**.
1. Para simplificar el control de versiones para las migraciones hemos añadido el atributo **NopMigrationAttribute** heredado de **MigrationAttribute** al código. Ahora puede simplemente especificar la fecha y la hora en que se creó la migración en lugar del número largo habitual.
1. También añadimos el atributo **SkipMigrationOnUpdateAttribute** que indica si una migración debe ser omitida durante el proceso de actualización.
1. Puede crear una tabla en la base de datos de dos maneras:
    * Utilice el método **Create.Table** en el método **Up** de su clase de migración y especifique todos los detalles utilizando los métodos de extensión.
    * Utilice el método **IMigrationManager.BuildTable\<T\>** en el método **Up** de su clase de migración y especifique todos los detalles, si es necesario, utilizando la implementación de las interfaces **IEntityBuilder** y **INameCompatibility** (en nopCommerce utilizamos este enfoque).
