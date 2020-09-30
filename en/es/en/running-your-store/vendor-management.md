---
title: Vendor management
uid: en/running-your-store/vendor-management
author: git.AndreiMaz
contributors: git.DmitriyKulagin, git.exileDev, git.ivkadp, git.mariannk
---

# Vendor management

*Vendedores* es una categoría especial de clientes que debe ser considerada por separado.

nopCommerce tiene herramientas para *multi-vendedores* y envíos directos que te permiten vender en línea sin tener que mantener existencias o enviar pedidos. En este caso, cada producto se asigna a un proveedor concreto cuyos datos (incluida la dirección de correo electrónico) se almacenan.

Cuando se realiza un pedido, se envía un correo electrónico a un proveedor de cada producto del pedido. El correo electrónico incluye los productos, las cantidades, etc. El vendedor envía el artículo al cliente en nombre del comerciante, que normalmente paga a cada uno de sus vendedores al final del mes.

Los productos de múltiples vendedores independientes aparecen en el catálogo de productos comunes y los visitantes de su sitio web pueden comprar en una tienda web, incluso si sus productos son suministrados por cientos de vendedores diferentes de todo el mundo.

Cada vendedor podría tener acceso a un panel de administración para gestionar sus productos, revisar los informes de ventas y pedir detalles sobre sus productos. Los vendedores no pueden ver las actividades de los demás.

El dinero va a la cuenta de comercio del administrador de la tienda que luego distribuye manualmente los fondos entre los vendedores según el historial de pedidos, que se rastrea y gestiona por separado para cada proveedor. De esta manera, el cliente sólo ve un cargo de la empresa principal.

El siguiente procedimiento describe cómo configurar y proporcionar un registro de proveedores con acceso al portal de proveedores.

## Establecer una cuenta de proveedor

Ir a **Clientes → Vendedores**. La ventana de *Vendedores* se muestra:

![Vendors](_static/vendor-management/vendor1.png)

Click **Add new**.

### Vendor info

![Add vendor](_static/vendor-management/vendor2.png)

En el panel *Información del proveedor*, defina los siguientes detalles del proveedor:

*  **Nombre** del vendedor.
* **Descripción** del vendedor.
* El correo electrónico del vendedor. Las notificaciones de "pedido realizado" serán enviadas a este correo.
* Marque la casilla de verificación **Activo** para activar el vendedor.
* Subir un vendedor **Imagen**.
* **Administre un comentario** un comentario opcional o información para uso interno.

> [!NOTE]
> 
> Algunas de las plantillas de mensajes de proveedores, como *OrderPaid.VendorNotification* y *OrderPlaced.VendorNotification*, están desactivadas por defecto. Vea cómo cambiar esto en [Message templates](xref:en/running-your-store/content-management/message-templates) section. 

### Vendor attributes

Cuando cree algunos atributos de proveedor adicionales, también se mostrará el panel *Atributos de proveedor*. 

Los propietarios de tiendas pueden crear atributos para un proveedor de la misma manera que para un producto. Esto permitiría a las tiendas de varios proveedores recopilar y mostrar más información sobre el proveedor a los clientes.

 Aprenda más sobre los atributos de los proveedores y cómo crearlos en la sección[Vendor attributes](#vendor-attributes)  más abajo.

### Address (optional)
In the *Address (optional)* panel enter the vendor address.

![Address (optional)](_static/vendor-management/address.jpg)

### Display

In the *Display* panel, define the following display parameters:

![Display](_static/vendor-management/vendor4.png)

* Para **Permitir a los clientes seleccionar el tamaño de la página** de una lista predefinida de opciones.
  * Si la casilla anterior está marcada, definir **Opciones de tamaño de página** (separadas por comas).
* Si la casilla de verificación anterior está desmarcada introduzca el **Tamaño de la página**.
* **Visualizar el pedido** del proveedor.

### SEO

Refer to [SEO panels](xref:en/running-your-store/search-engine-optimization#seo-panels) section in order to set up SEO.

![SEO](_static/vendor-management/seo.jpg)

## Asignar un proveedor a un registro de clientes

Este paso es opcional y sólo es necesario si desea que sus proveedores puedan acceder a su portal de administración y gestionar sus productos, pedidos, etc.

Si no desea que los proveedores tengan acceso al área de administración, ignore este paso para permitir que el propietario de la tienda gestione todas las asignaciones de proveedores.

Ir a **Clientes → Clientes**. La ventana de *Clientes* se muestra:

![Customers](_static/vendor-management/vendor7.png)

Ccrear un nuevo cliente o hacer clic en **Editar** al lado de un registro de cliente al que quiere asignar un proveedor. Para obtener más información sobre la creación de un cliente, consulte [Add a new customer](xref:en/running-your-store/customer-management/managing-customers#add-a-new-customer).

* En el panel *Información del cliente*, asegúrate de que el rol de cliente de *Vendedores* está seleccionado en el campo **Roles del cliente**.
  > [!NOTE]
  > 
  > Una cuenta de cliente de proveedor no puede pertenecer al rol de cliente predeterminado de *Administradores*.

* En el panel *Información del cliente*, busque el campo **Administrador del proveedor**. Seleccione un registro de proveedor creado previamente.

![Edit customer](_static/vendor-management/edit-customer.jpg)

Una vez configurada la cuenta de cliente del proveedor, éste puede utilizarla para gestionar productos, pedidos, envíos y ver informes. El enlace *Administración* en la parte superior de la tienda pública se mostrará después de iniciar sesión.

> [!TIP]
> 
> [YouTube tutorial: Managing vendors](https://www.youtube.com/watch?v=MH6r6tqfLF8&list=PLnL_aDfmRHwsbhj621A-RFb1KnzeFxYz4&index=9)


## Ajustes del proveedor

En esta sección se describe cómo definir la configuración del proveedor de su tienda. Esto incluye el número de proveedores que se deben mostrar, si se debe mostrar o no el proveedor en las páginas de detalles de los productos de la tienda y más.

Vaya a **Configuración → Ajustes → Ajustes de proveedor**.

Esta página permite la configuración de varias tiendas, lo que significa que se pueden definir los mismos ajustes para todas las tiendas o que pueden ser diferentes de una tienda a otra. Si desea administrar la configuración de una tienda determinada, elija su nombre en la lista desplegable de configuración de varias tiendas y marque todas las casillas de verificación necesarias en el lado izquierdo para establecer un valor personalizado para ellas. Para obtener más detalles, consulte [Multi-store](xref:en/getting-started/advanced-configuration/multi-store).
	
### Common

En el panel *Común* defina los siguientes ajustes del proveedor:
![Common](_static/vendor-management/vendorsettings1.png)

* **Permitir a los clientes solicitar una cuenta de proveedor**. En primer lugar, la solicitud de un proveedor es llenada por un usuario, creando así una cuenta de proveedor. Luego, la solicitud se presenta al propietario de la tienda (a través de una notificación por correo electrónico) para ser aceptada.
  > [!NOTE]
  > 
  > A store owner has to add an appropriate customer record to "Vendors" role manually if he wants to grant access to the admin area. Read about it in the [Assigning a proveedor a un registro de cliente](#asignación de un proveedor a un registro de cliente) sección anterior.

  * Si la casilla de verificación anterior está marcada, puede marcar la casilla **Términos de servicio** para exigir a los proveedores que acepten los términos de servicio durante el registro.
    > [!NOTE]
    >
    > Para editar estos términos de servicio vaya a **Gestión de contenidos → Temas (páginas)**. Encuentre el artículo **Términos de Servicio del Proveedor** y haga clic en **Editar**. Lea más sobre ello en el [Topics (pages)](xref:en/running-your-store/content-management/topics-pages) section.

* **Permitir a los vendedores editar la información** permite a los vendedores proporcionar información personal en la tienda pública.
  * Elija si **Notificar sobre los cambios de información del vendedor** para notificar a un administrador sobre los cambios de información del vendedor.

* **Máximo número de productos** por vendedor.
* **Permitir a los vendedores importar productos** permite a los vendedores importar productos.

### Catálogo

En el panel *Catálogo* defina los siguientes ajustes del proveedor:
![Catalog](_static/vendor-management/vendorsettings2.png)

* **Permitir a los clientes contactar con los vendedores** (enviar correos electrónicos utilizando formularios de contacto). Esta funcionalidad está disponible en una página de detalles del vendedor en la tienda pública.
* **Permitir la búsqueda por vendedor** a los clientes, en una página de búsqueda avanzada.
* Elija si desea **Mostrar el vendedor en la página de detalles del producto** (si está asociado).
* Elija si desea **Mostrar el nombre del proveedor en la página de detalles del pedido** (si está asociada).
* **Mostrar el número de proveedores** en el bloque de navegación de proveedores en el área de administración.

### Atributos del proveedor

Puede crear cualquier número de atributos de proveedor. Algunos atributos diferentes que podrían ser creados serían el nombre de la empresa, el sitio web, etc.

![Vendor attributes](_static/vendor-management/vendorsettings3.png)

#### Añadir un nuevo atributo
Haga clic en **Agregar nuevo** para crear un nuevo atributo de proveedor así como sus valores. Se mostrará la ventana *Agregar nuevo atributo de proveedor*, de la siguiente manera:

![Add new](_static/vendor-management/vendorsettings4.png)

En el panel de *Información de atributos*, defina la siguiente información:
* **Nombre** - el nombre del atributo del vendedor.
* **Required** - cuando se requiere un atributo, los vendedores deben elegir un valor de atributo apropiado antes de poder continuar.
* En la lista desplegable **Tipo de control**, seleccione el método requerido para mostrar el valor de atributo: *Lista desplegable, Lista de botones de radio, Casilla de verificación, Casilla de texto, Casilla de texto multilínea, Casilla de verificación de sólo lectura*.
* **Orden de visualización** - el orden de visualización del atributo del proveedor.

> [!NOTE]
> 
> Las listas desplegables, las listas de radio, la casilla de verificación y la casilla de verificación de sólo lectura requieren que el dueño de la tienda defina los valores. Los tipos de control de caja de texto y de caja de texto de varias líneas no requieren que el propietario de la tienda defina valores, ya que los proveedores deberán rellenar estos campos de caja de texto.

Haga clic en **Save and continue edit** para proceder al panel de *Valores*.

#### Agregar un nuevo valor de atributo

En el panel *Valores*, haga clic en **Agregar un nuevo valor de atributo** para crear un nuevo valor de atributo.

![Add a new attribute values](_static/vendor-management/vendorsettings5.png)

En la ventana *Añadir un nuevo valor de atributo*, defina la siguiente información:

* **Nombre** - el nombre del valor de atributo.
* Marque la casilla de verificación **Pre-seleccionado**, para indicar que el valor de atributo está preseleccionado para un cliente.
* **Display order** - mostrar el número de orden del valor de atributo.

Puede editar y eliminar los valores de atributo haciendo clic en los botones correspondientes junto a los valores de atributo en el panel *Valores*.

Haga clic en **Guardar**. El nuevo atributo se mostrará en la tienda pública.