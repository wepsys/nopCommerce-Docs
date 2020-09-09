---
title: Adding CSS and JS resource files into nopCommerce Plugin
uid: en/developer/plugins/resource-files
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Agregar archivos de recursos CSS y JS al complemento nopCommerce

Para cargar los archivos de recursos correctamente, debe agregar sus referencias en los archivos de vista de su complemento.

Puedes usar `Html.AddScriptParts()` O `Html.AddCssFileParts()` métodos de ayuda.

- `Html.AddCssFileParts()`
- `Html.AddScriptParts()`

Puede consultar más detalles sobre estos métodos yendo a su definición en sus proyectos de nopCommerce.
```csharp
@{
     //Loading CSS file
     Html.AddCssFileParts(ResourceLocation.Head, "~/Plugins/{PluginName}/Content/{CSSFileName.Css}");

     //Loading js file
     //Third parameter value indicating whether to exclude this script from bundling
     Html.AddScriptParts(ResourceLocation.Footer, "~/Plugins/{PluginName}/Scripts/{JSFileName.js}", true);
}
```

Si desea agregar un enlace de recursos en el encabezado, puede usar ResourceLocation.Head y para el pie de página puede usar *ResourceLocation.Footer*.
