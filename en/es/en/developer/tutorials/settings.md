---
title: Settings API
uid: en/developer/tutorials/settings
author: git.AndreiMaz
contributors: git.exileDev
---

# Ajustes de la API

Como cualquier otra plataforma web, nopCommerce tiene ajustes como "Nombre de la tienda" o "Pago en una página habilitado". Hay dos maneras de administrar la configuración en nopCommerce.

Puede utilizar los métodos **GetSettingByKey** y **SetSetting** de implementación de **ISettingService** para cargar y guardar configuraciones individuales. El enfoque preferido para manejar las configuraciones en nopCommerce es crear una nueva implementación de la interfaz **ISettings**. Cada configuración estará representada por una propiedad C# y los desarrolladores deben confiar en las clases de configuración para ser inyectadas a través del constructor cuando sea necesario. A continuación se muestra un ejemplo de clase de configuración.

```csharp
public class MediaSettings : ISettings
{
    public int AvatarPictureSize { get; set; }
    public int ProductThumbPictureSize { get; set; }
    public int ProductDetailsPictureSize { get; set; }
    public int ProductThumbPictureSizeOnProductDetailsPage { get; set; }
    public int ProductVariantPictureSize { get; set; }
    public int CategoryThumbPictureSize { get; set; }
    public int ManufacturerThumbPictureSize { get; set; }
    public int CartThumbPictureSize { get; set; }
    public bool DefaultPictureZoomEnabled { get; set; }
    public int MaximumImageSize { get; set; }
}
```
