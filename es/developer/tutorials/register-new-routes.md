---
title: How do I register new routes?
uid: es/developer/tutorials/register-new-routes
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Registrar nuevas rutas

El enrutamiento de ASP.NET Core es responsable de asignar las solicitudes entrantes del navegador a determinadas acciones del controlador MVC. Puede encontrar más información sobre el enrutamiento [aquí](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-3.1). nopCommerce tiene una interfaz IRouteProvider que se utiliza para el registro de rutas durante el inicio de la aplicación. Todas las rutas principales están registradas en la clase RouteProvider ubicada en el proyecto `Nop.Web`.

```csharp
 public void RegisterRoutes(IEndpointRouteBuilder endpointRouteBuilder)
{
    var pattern = string.Empty;
    if (DataSettingsManager.DatabaseIsInstalled)
    {
        var localizationSettings = endpointRouteBuilder.ServiceProvider.GetRequiredService<LocalizationSettings>();
        if (localizationSettings.SeoFriendlyUrlsForLanguagesEnabled)
        {
            var langservice = endpointRouteBuilder.ServiceProvider.GetRequiredService<ILanguageService>();
            var languages = langservice.GetAllLanguages().ToList();
            pattern = "{language:lang=" + languages.FirstOrDefault().UniqueSeoCode + "}/";
        }
    }

    //home page
    endpointRouteBuilder.MapControllerRoute("Homepage", pattern, new { controller = "Home", action = "Index" });
}
```

Puede crear tantas clases de RouteProvider como necesite. Por ejemplo, si su complemento tiene algunas rutas personalizadas que desea registrar, cree una nueva clase que implemente la interfaz IRouteProvider y registre las rutas específicas para su nuevo complemento.
