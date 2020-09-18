---
title: Updating an existing entity. How to add a new property.
uid: en/developer/tutorials/update-existing-entity
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Actualización de una entidad existente. Cómo agregar una nueva propiedad

Este tutorial cubre cómo agregar una propiedad a la entidad "Categoría" que se envía con el código fuente de nopCommerce.

## El modelo de datos

Las entidades tendrán dos clases que se utilizan para asignar registros a una tabla. La primera clase define las propiedades, campos y métodos consumidos por la aplicación web.

`` sh
Ubicación del sistema de archivos: [Project-Root]\Libraries\Nop.Core\Domain\Catalog\Category.cs
Montaje: Nop.Core
Ubicación de la solución: Nop.Core.Domain.Catalog.Category.cs
''

La segunda clase se utiliza para asignar las propiedades definidas en la clase anterior a sus respectivas columnas SQL. La clase de mapeo también es responsable de mapear relaciones entre diferentes tablas SQL.

```sh
File System Location: [Project-Root]\Libraries\Nop.Data\Mapping\Builders\Catalog\CategoryBuilder.cs
Assembly: Nop.Data
Solution Location: Nop.Data.Mapping.Builders.Catalog.CategoryBuilder.cs
```

Pero te recomiendo que lo uses solo para tus propias clases de entidad. En nuestro caso, usaremos el mecanismo de migración en lugar de la clase de mapeo.

Agregue la siguiente propiedad a la clase Categoría.

```csharp
public string SomeNewProperty { get; set; }
```

Agregue la nueva clase (Nop.Data.Migrations.AddSomeNewProperty) con el siguiente código: 

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
> Dado que las migraciones solo aparecieron en nopCommerce 4.30, no implementa la llamada al procedimiento de actualización. Por lo tanto, debe agregar el siguiente código al método **ApplicationBuilderExtensions.StartEngine**

```csharp
var migrationManager = EngineContext.Current.Resolve<IMigrationManager>();
migrationManager.ApplyUpMigrations();
```

> El código especificado debe agregarse antes de las líneas:

```csharp
//update plugins
pluginService.UpdatePlugins();
```

## El modelo de presentación

El modelo de presentación se utiliza para transportar información desde un controlador a la vista (lea más en asp.net/mvc). Los modelos tienen otro propósito; definición de requisitos.

Configuramos nuestra base de datos para almacenar solo 255 caracteres para SomeNewProperty. Si intentamos guardar un SomeNewProperty con 300 caracteres, la aplicación se romperá (o truncará el texto). Queremos que la aplicación proteja a los usuarios de las fallas lo mejor que podamos, y nuestros modelos de vista ayudan a hacer cumplir requisitos como la longitud de las cadenas.

```sh
Ubicación del sistema de archivos: [Project Root]\Presentation\Nop.Web\Areas\Admin\Models\Catalog\CategoryModel.cs
Assembly: Nop.Admin
Ubicación de la solución: Nop.Web.Areas.Admin.Models.Catalog.CategoryModel.cs
```

La clase de validación se utiliza para validar los datos almacenados dentro de la clase de modelo (por ejemplo, campos obligatorios, longitud máxima y rangos obligatorios).

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Validators\Catalog\CategoryValidator.cs
Assembly: Nop.Web
Solution Location: Nop.Web.Areas.Admin.Validators.Catalog.CategoryValidator.cs
```

Add the property to our view model.

```csharp
// The NopResourceDisplayName provides the "key" used during localization
// Keep an eye out for more about localization in future blogs
[NopResourceDisplayName("Admin.Catalog.Categories.Fields.SomeNewProperty")]
public string SomeNewProperty { get; set; }
```

The requirements code will be added in the constructor of the validator.

```csharp
//I think this code can speak for itself
RuleFor(m => m.SomeNewProperty).Length(0, 255);
```

## The view

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Views\Category\ _CreateOrUpdate.Info.cshtml
Assembly: Nop.Web
```

Views contain the html for displaying model data. Place this html under the "PictureId" section.

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

En este caso, el controlador es responsable de asignar el modelo de datos de dominio a nuestro modelo de vista y viceversa. La razón por la que elijo el modelo de categoría para actualizar es por la simplicidad. Quiero que esto sea una introducción a la plataforma nopCommerce y me gustaría que sea lo más simple posible.

```sh
File System Location: [Project Root]\Presentation\Nop.Web\Areas\Admin\Controllers\CategoryController.cs
Assembly: Nop.Admin
Solution Location:
Nop.Web.Areas.Admin.Controllers.CategoryController.cs
```

Vamos a hacer tres actualizaciones a la clase CategoryController.

* Modelo de datos → Ver modelo
* Crear modelo de vista → Modelo de datos
* Editar modelo de vista → Modelo de datos

Normalmente, escribiría pruebas para el siguiente código y verificaría que el mapeo del modelo funcione correctamente, pero omitiré las pruebas unitarias para que sea más simple.

En los métodos apropiados ("Crear", "Editar" o "PrepareSomeModel") agregue el código para establecer esta propiedad. En la mayoría de los casos, no es necesario porque AutoMapper lo maneja automáticamente en el método .ToModel ().

En el método público para guardar la entidad (generalmente: "Crear" o "Editar" se reunióhods with [HttpPost] attribute)

```csharp
// Edit View Model → Data Model
category.SomeNewProperty = model.SomeNewProperty;
```

## Solución de problemas

* Recrear la base de datos. Ya sea su propio script SQL personalizado o use el instalador nopCommerce.
* Detenga el servidor web de desarrollo entre cambios de esquema.
* Publica un comentario detallado sobre[nuestros foros](http://www.nopcommerce.com/boards/).
