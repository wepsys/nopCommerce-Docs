---
title: How to add a menu item into the administration area from a plugin
uid: en/developer/plugins/menu-item
author: git.AndreiMaz
contributors: git.Sandeep911, git.DmitriyKulagin, git.exileDev
---

# Cómo agregar un elemento de menú en el área de administración desde un plungin

En nopCommerce, el menú de administración se crea a partir del archivo *sitemap.config* que se encuentra en la carpeta *~/Areas /Admin*.

Para hacer lo mismo, puede usar el siguiente código de muestra que debe agregar en el archivo cs de sus complementos. Primero, implemente la interfaz IAdminMenuPlugin en la clase principal de su complemento.

Luego, también puede poner cualquier lógica de seguridad (ACL) en este método. Por ejemplo, valide si el cliente actual tiene el permiso "Administrar complementos".

```csharp
 public class CustomPlugin : BasePlugin, IAdminMenuPlugin
 {

    public void ManageSiteMap(SiteMapNode rootNode)
    {
        var menuItem = new SiteMapNode()
        {
            SystemName = "YourCustomSystemName",
            Title = "Plugin Title",
            ControllerName = "ControllerName",
            ActionName = "List",
            Visible = true,
            RouteValues = new RouteValueDictionary() { { "area", null } },
        };
        var pluginNode = rootNode.ChildNodes.FirstOrDefault(x => x.SystemName == "Third party plugins");
        if(pluginNode != null)
            pluginNode.ChildNodes.Add(menuItem);
        else
            rootNode.ChildNodes.Add(menuItem);
    }

}

```

In version 2.00-3.50 you should do it the following way:

```csharp
public bool Authenticate()
{
    return true;
}

public  SiteMapNode BuildMenuItem() //SiteMapNode es una clase en Nop.Web.Framework.Menu
{
   var menuItemBuilder = new SiteMapNode()
   {
       Title = "Title For Menu item",   // Título de su elemento de menú personalizado
       Url = "Path of action link", //Ruta del enlace de acción
       Visible = true,
       RouteValues = new RouteValueDictionary() { {"Area", "Admin"} }
   };
    var SubMenuItem = new SiteMapNode()   // agregar menú personalizado infantil
   {
       Title =  "Title For Menu Child menu item", //   Título de su elemento de submenú
       ControllerName = "Your Controller Name", // Su nombre de controlador
       ActionName = "Configure", //Nombre de la acción
       Visible = true,
       RouteValues = new RouteValueDictionary() { {"Area", "Admin"} },
   };
   menuItemBuilder.ChildNodes.Add(SubMenuItem);

   return menuItemBuilder;
}
```

En el código anterior, puede encontrar comentarios en los que necesita reemplazar valores según sus requisitos. Además, el código anterior también explica cómo puede agregar elementos del menú secundario dentro del menú principal.
