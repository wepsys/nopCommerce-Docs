---
title: Manual (fixed or by country/state/zip)
uid: en/getting-started/configure-taxes/tax-providers/manual
author: git.AndreiMaz
contributors: git.exileDev
---

# Manual (fijo o por país/estado/zip)

Para configurar el proveedor de impuestos manual (fijo o por país/estado/código postal), vaya a **Configuración → Proveedores de impuestos**.

![Proveedores de impuestos](_static/manual/tax-Suppliers.png)

Haga clic en **Configurar** en la línea del proveedor **Manual (fijo o por país/estado/código postal)** para editar las tasas de impuestos.
Puede cambiar *Tasa fija* cálculo de impuestos a *País/estado/código postal* cálculo de impuestos haciendo clic en el botón en la parte superior de la página.

## Tipo de interés fijo

Elija la configuración **Tarifa fija** utilizando el conmutador en la parte superior de la página.

![Configurar](_static/manual/configure.jpg)

En esta página puede ver las categorías de impuestos creadas previamente. Haga clic en **Editar** junto a cada categoría e ingrese las tasas de porcentaje. Luego haga clic en el botón **Actualizar**.

Asegúrese de que sus productos tengan asignada una categoría de impuestos en sus [páginas de productos](xref:en/running-your-store/catalog/products/add-products).

![Producto](_static/manual/product.jpg)

> [!NOTA]
>
> Esta sección muestra solo categorías de impuestos creadas previamente. Lea cómo crear nuevas categorías a continuación: [configurar categorías de impuestos](#configure-tax-categorías).

## Por país

Elija la configuración **Por país** usando el conmutador en la parte superior de la página.

![Por país](_static/manual/tax-by-country.png)

Defina la nueva tasa impositiva de la siguiente manera:

* Seleccione la **Tienda** para la que está definida la tarifa. Seleccione un * para aplicar esta tarifa a todas las tiendas.
* Seleccione el **País** para el que se define la tasa impositiva.
* Seleccione el **Estado/provincia** para el que se define la tasa impositiva. Si se selecciona un asterisco (*), esta tasa impositiva se aplicará a todos los clientes del país seleccionado independientemente del estado.
* Ingrese el código **Zip** de un área para la cual se define la tasa de impuestos. Si este campo está vacío, esta tasa de impuestos se aplicará a todos los clientes del país o estado seleccionado, independientemente del código postal.
* Seleccione la **categoría de impuestos** a la que aplicar la tasa de impuestos.
* En el campo **Porcentaje**, ingrese el porcentaje requerido.

Haga clic en **Agregar tasa impositiva**. Se muestra la nueva tasa impositiva de la siguiente manera:

![Agregar tasa de impuestos](_static/manual/add-tax-rate.png)

> [!NOTA]
>
> Esta sección muestra solo categorías de impuestos creadas previamente. Lea cómo crear nuevas categorías a continuación: [configurar categorías de impuestos](#configure-tax-categorías).

## Configurar categorías de impuestos

Para definir las categorías de impuestos, vaya a **Configuración → Categorías de impuestos**. Se muestra la ventana *Categorías de impuestos*:

![Categorías de impuestos](_static/manual/tax-categories.jpg)

Para agregar una nueva categoría de impuestos, ingrese la categoría **Nombre** y el **Orden de visualización** de esta clasificación de impuestos en la parte inferior del panel. En el campo **Orden de visualización**, el valor 1 representa la parte superior de la lista. Luego haga clic en **Agregar nuevo registro** para guardar la nueva categoría de impuestos.