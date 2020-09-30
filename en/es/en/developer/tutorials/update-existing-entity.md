---
title: Updating an existing entity. How to add a new property.
uid: en/developer/tutorials/update-existing-entity
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Actualizar una entidad existente. Cómo añadir una nueva propiedad

Este tutorial cubre cómo añadir una propiedad a la entidad "Categoría" que se envía con el código fuente de nopCommerce.

## El modelo de datos

Las entidades tendrán dos clases que se usan para mapear los registros a una tabla. La primera clase define las propiedades, campos y métodos consumidos por la aplicación web.

```sh
File System Location: [Project Root]\Libraries\Nop.Core\Domain\Catalog\Category.cs
Assembly: Nop.Core
Solution Location: Nop.Core.Domain.Catalog.Category.cs
```

La segunda clase se utiliza para mapear las propiedades definidas en la clase anterior a sus respectivas columnas SQL. La clase de mapeo también es responsable de mapear las relaciones entre las diferentes tablas SQL.

```sh
File System Location: [Project Root]\Libraries\Nop.Data\Mapping\Builders\Catalog\CategoryBuilder.cs
Assembly: Nop.Data
Solution Location: Nop.Data.Mapping.Builders.Catalog.CategoryBuilder.cs
```

Pero te recomiendo que lo uses sólo para tus propias clases de entidad. En nuestro caso, usaremos el mecanismo de migración en lugar de la clase de mapeo.

Añade la siguiente propiedad a la clase de categoría.

```csharp
public string SomeNewProperty { get; set; }
```

Añade la nueva clase (Nop.Data.Migrations.AddSomeNewProperty) con el siguiente código:  

```csharp
using FluentMigrator;
using Nop.Core.Domain.Catalog;

namespace Nop.Data.Migrations
{
    [NopMigration("2020/05/25 11:24:16:2551770", "Category. Add some new property")]
    public class AddSomeNewProperty: AutoReversingMigration
    {
        /// <summary>Collect the UP migration expressions</summary>
        public override void Up()
        {
            Create.Column(nameof(Category.SomeNewProperty))
            .OnTable(nameof(Category))
            .AsString(255)
            .Nullable();
        }
    }
}
```

> [!NOTE]
> Como las migraciones sólo aparecieron en el nopCommerce 4.30, no implementa la llamada de procedimiento de actualización. Por lo tanto, es necesario añadir el siguiente código al método **ApplicationBuilderExtensions.StartEngine**

```csharp
var migrationManager = EngineContext.Current.Resolve<IMigrationManager>();
migrationManager.ApplyUpMigrations();
```

> El código especificado debe ser añadido antes de las líneas:

```csharp
//update plugins
pluginService.UpdatePlugins();
```

## El modelo de presentación

El modelo de presentación se utiliza para transportar la información desde un controlador a la vista (lea más en asp.net/mvc). Los modelos tienen otro propósito; definir los requisitos.

Configuramos nuestra base de datos para almacenar sólo 255 caracteres para el SomeNewProperty. Si intentamos guardar un CiertoNuevoPropiedad con 300 caracteres la aplicación se romperá (o truncará el texto). Queremos que la aplicación proteja a los usuarios de los fallos lo mejor que podamos, y nuestros modelos de vista ayudan a hacer cumplir requisitos como la longitud de la cadena.

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Models\Catalog\CategoryModel.cs
Assembly: Nop.Admin
Solution Location: Nop.Web.Areas.Admin.Models.Catalog.CategoryModel.cs
```

La clase validadora se utiliza para validar los datos almacenados dentro de la clase modelo (por ejemplo, los campos obligatorios, la longitud máxima y los rangos requeridos).

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Validators\Catalog\CategoryValidator.cs
Assembly: Nop.Web
Solution Location: Nop.Web.Areas.Admin.Validators.Catalog.CategoryValidator.cs
```

Añade la propiedad a nuestro modelo de vista.

```csharp
// The NopResourceDisplayName provides the "key" used during localization
// Keep an eye out for more about localization in future blogs
[NopResourceDisplayName("Admin.Catalog.Categories.Fields.SomeNewProperty")]
public string SomeNewProperty { get; set; }
```

El código de requisitos se añadirá en el constructor del validador.

```csharp
//I think this code can speak for itself
RuleFor(m => m.SomeNewProperty).Length(0, 255);
```

## The view

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Views\Category\ _CreateOrUpdate.Info.cshtml
Assembly: Nop.Web
```

Las vistas contienen el html para mostrar los datos del modelo. Coloca este html en la sección "PictureId".

```csharp
<div class="form-group">
     <div class="col-md-3">
        <nop-label asp-for="SomeNewProperty" />
     </div>
     <div class="col-md-9">
        <nop-editor asp-for="SomeNewProperty" />
        <span asp-validation-for="SomeNewProperty"></span>
     </div>
 </div>
```

## El controlador

En este caso el controlador es responsable de mapear el modelo de datos del dominio a nuestro modelo de vista y viceversa. La razón por la que elijo el modelo de categoría para actualizar es por la simplicidad. Quiero que esto sea una introducción a la plataforma nopCommerce y me gustaría mantenerlo lo más simple posible.

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Controllers\CategoryController.cs
Assembly: Nop.Admin
Solution Location:
Nop.Web.Areas.Admin.Controllers.CategoryController.cs
```

Vamos a hacer tres actualizaciones a la clase de Controlador de Categoría.

* Modelo de datos → Ver Modelo
* Crear Modelo de Vista → Modelo de Datos
* Editar Ver Modelo → Modelo de Datos

Normalmente escribiría pruebas para el siguiente código y verificaría que el mapeo del modelo funciona correctamente, pero me saltaré las pruebas de la unidad para mantenerlo simple.

En los métodos apropiados ("Create", "Edit", o "PrepareSomeModel") agregue el código para establecer esta propiedad. En la mayoría de los casos no es necesario porque se maneja automáticamente por el AutoMapper en el método .ToModel().

In the public method to save entity (usually: "Create" or "Edit" methods with [HttpPost] attribute)

```csharp
// Edit View Model → Data Model
category.SomeNewProperty = model.SomeNewProperty;
```

## Solución de problemas

* Recrear la base de datos. O bien tu propio script SQL personalizado o usa el instalador de nopCommerce.
* Detener el servidor web de desarrollo entre los cambios de esquema.
* Publicar un comentario detallado sobre [our forums](http://www.nopcommerce.com/boards/).
