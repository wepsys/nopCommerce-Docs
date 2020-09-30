---
title: How do I register new routes?
uid: en/developer/tutorials/register-new-routes
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev
---

# Registrar nuevas rutas

El enrutamiento del núcleo ASP.NET es responsable de mapear las solicitudes entrantes del navegador a acciones particulares del controlador MVC. Puedes encontrar más información sobre el enrutamiento [aquí](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-3.1). nopCommerce tiene una interfaz IRouteProvider que se utiliza para el registro de rutas durante el inicio de la aplicación. Todas las rutas principales se registran en la clase RouteProvider ubicada en el proyecto `Nop.Web`.

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

Puedes crear tantas clases de RouteProvider como necesites. Por ejemplo, si tu plugin tiene algunas rutas personalizadas que quieres registrar, entonces crea una nueva clase implementando la interfaz de IRouteProvider y registra las rutas específicas de tu nuevo plugin..
