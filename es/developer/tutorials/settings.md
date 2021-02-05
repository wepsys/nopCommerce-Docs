---
title: Settings API
uid: es/developer/tutorials/settings
author: git.AndreiMaz
contributors: git.exileDev
---

# API de configuración

Como cualquier otra plataforma de sitios web, nopCommerce tiene configuraciones como "Nombre de la tienda" o "Pago de una página habilitado". Hay dos formas de administrar la configuración en nopCommerce.

Puede utilizar los métodos **GetSettingByKey** y **SetSetting** de la implementación de **ISettingService** para cargar y guardar configuraciones individuales. El enfoque preferido para manejar la configuración en nopCommerce es crear una nueva implementación de la interfaz **ISettings**. Cada configuración estará representada por una propiedad de C# y los desarrolladores deben confiar en que las clases de configuración se inyecten a través del constructor cuando sean necesarias. A continuación se muestra una clase de configuración de ejemplo.

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
