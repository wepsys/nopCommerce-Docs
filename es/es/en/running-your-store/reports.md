---
title: Reports
uid: en/running-your-store/reports
author: git.AndreiMaz
contributors: git.exileDev, git.mariannk
---

# Informes

Los informes son importantes para la gestión, ya que permiten supervisar el rendimiento de la tienda, hacer un seguimiento de las métricas clave y apoyar la toma de decisiones. Los informes de nopCommerce proporcionan acceso a la información sobre ventas y clientes.

## Dashboard

El tablero es la primera página que se ve al acceder al área de administración. Le permite ver las estadísticas de su tienda, incluyendo el número total de pedidos que se procesaron durante el período de tiempo que usted elija (año, mes, semana), clientes registrados, productos de bajo stock, los productos más populares de su tienda, etc.

![Dashboard](_static/reports/dashboard.png)

El tablero de mandos consta de varios bloques:

### nopCommerce news
Muestra las noticias generales de nopCommerce como los lanzamientos de nuevas versiones.
![News](_static/reports/news.png)

### Common statistics 
![Common](_static/reports/common.png)

Aquí puede encontrar enlaces a informes más detallados:
* Ventas → Pedidos
* Ventas → Solicitudes de devolución
* Clientes → Clientes registrados
* Informes → Baja de existencias

### Orders
Este diagrama le permite saber el número de pedidos que fueron procesados en la última semana, mes, año.
![Orders](_static/reports/orders.jpg)

### Nuevos clientes
Este diagrama muestra el número de clientes registrados en la última semana, mes, año.
![New customers](_static/reports/customers.jpg)

### Los totales de la orden
Esta sección le permite conocer el total de pedidos que fueron procesados en el último día, semana, mes, año. Los pedidos se muestran por el estado del pedido.
![Order totals](_static/reports/order-totals.png)

### Pedidos incompletos
Esta sección permite conocer el número de pedidos que actualmente están incompletos.
![Orders incomplete](_static/reports/order-incomplete.png)

### Últimos pedidos
La sección de últimos pedidos muestra los últimos pedidos realizados.
![Latest orders](_static/reports/order-latest.png)

### Popular search keywords
This block displays most used keywords.

![Keywords](_static/reports/keywords.png)

### Bestsellers
This section displays the bestsellers by quantity and by amount.
![Bestsellers](_static/reports/bestsellers.png)


## Informe del país
El informe del país contiene una lista de pedidos que incluye el número de pedidos y la suma total de los mismos en cada país. Esto permite a los propietarios de las tiendas ver los pedidos por país.

Para ver los informes de los países, vaya a **Informes → Informe del país**.

![Country report](_static/reports/country-report.png)

Para configurar el informe, introduzca uno o más de los siguientes criterios de búsqueda:
* **Fecha de inicio** de la búsqueda.
* **Fecha de finalización** para la búsqueda.
* **Estado del pedido**, como *Todo*, *Pendiente*, *Procesando*, *Completo*, o *Cancelado*.
* **Estado de pago**, como *Todo*, *Pendiente*, *Autorizado*, *Pagado*, *Reembolsado*, *Reembolsado parcialmente*, o *Anulado*.

Then click **Run report**.


## Informes de los clientes
Los informes de los clientes dan al dueño de la tienda información general sobre los clientes registrados y sus pedidos. Puedes encontrar diferentes informes en el menú **Reportes → Informes de clientes**.

### Clientes registrados
Para ejecutar este informe vaya a **Informes → Informes de clientes → Clientes registrados**.
Este informe muestra el número de clientes registrados durante un cierto período.
Puede rastrear el número de usuarios registrados en el último día, semana, dos semanas, mes y año.

![Registered customers](_static/reports/customer-registered.png)

### Clientes por total del pedido
Para ejecutar este informe vaya a **Informes → Informes de clientes → Clientes por total de pedidos**.
En este informe se puede ver el total de pedidos gastados por los clientes y el número de pedidos de los clientes.

![Customers by order total](_static/reports/Customers-by-order-total.png)

Introduzca uno o varios criterios de búsqueda para elaborar un informe:
* Registro **Fecha de inicio**.
* Registro **Fecha de finalización**.
* **Estado del pedido**, como *Todo*, *Pendiente*, *Procesando*, *Completo*, o *Cancelado*.
* **Estado de pago**, como *Todo*, *Pendiente*, *Autorizado*, *Pagado*, *Reembolsado*, *Reembolsado parcialmente*, o *Anulado*.
* **Estado de envío** como *Todo*, *Envío no requerido*, *No enviado todavía*, *Enviado parcialmente*, *Enviado*, *Entregado*.

Entonces haz clic en **Run report**.

### Clientes por número de pedidos
Para ejecutar este informe vaya a **Informes → Informes de clientes → Clientes por número de pedidos**.
Este informe muestra los 20 principales clientes según el número total de pedidos emitidos.

![Customers by number of orders](_static/reports/Customers-by-number-of-orders.png)

Enter one or several search criteria to compile a report:

* Registro **Fecha de inicio**.
* Registro **Fecha de finalización**.
* **Estado del pedido**, como *Todo*, *Pendiente*, *Procesando*, *Completo*, o *Cancelado*.
* **Estado de pago**, como *Todo*, *Pendiente*, *Autorizado*, *Pagado*, *Reembolsado*, *Reembolsado parcialmente*, o *Anulado*.
* **Estado de envío** como *Todo*, *Envío no requerido*, *No enviado todavía*, *Enviado parcialmente*, *Enviado*, *Entregado*.

Entonces haz clic en **Run report**.


## Informe de bajas existencias

El informe de existencias bajas contiene una lista de productos que se encuentran actualmente en existencias. En el ejemplo que se muestra a continuación, la cantidad mínima de existencias se fijó en 20 y la cantidad de existencias es 0, por lo que se genera un informe de existencias bajas para este producto. Puede configurar las opciones de existencias bajas al agregar el producto.

Para ver los informes de existencias bajas, vaya a **Reportes → Existencias bajas**. La ventana del informe de *Baja Existencias* se muestra de la siguiente manera: 
![Low stock report](_static/reports/low-stock-reports.png)

Los informes de existencias bajas podrían ser filtrados por la propiedad **Publicada**, que representa la propiedad *Publicada* de los productos.

En la tabla que se muestra, haga clic en **Ver** para ver la página de detalles del producto donde se puede actualizar la cantidad de existencias.


## Los más vendidos y nunca comprados

Conocer los productos más vendidos y los que nunca se han comprado es muy importante para cualquier propietario de una tienda. 

En primer lugar, esto puede ayudar a tomar mejores decisiones de compra: puede ampliar sus artículos populares y excluir los impopulares de su lista de productos. Cuando analice, considere, por ejemplo, si ciertos colores se venden más rápido, o si las ventas de sus productos dependen de una temporada. 

En segundo lugar, definir los productos más y menos vendidos puede ayudarte a *reevaluar el diseño y la comercialización del producto*. Tal vez tus mejores artículos se venden más rápido sólo por su colocación en tu tienda web, o por una mejor descripción. Piensa en diferentes opciones y pruébalas. Para hacerlo de manera más efectiva, comprométase con sus clientes. *Conduce diferentes encuestas* para averiguar por qué se prefieren los artículos más vendidos, qué los hace especiales para tus compradores. Utilice los conocimientos para mejorar su marketing y aumentar las ventas.

### Los más vendidos
Para ver los bestsellers en nopCommerce, ve a **Reportes → Bestsellers**. Introduzca uno o más de los siguientes criterios de búsqueda para ejecutar el informe:
* **Fecha de inicio** y/o **Fecha de finalización**.
* **Store**, si quieres seleccionar una de tus tiendas.
* **Estado del pedido**, como *Todo*, *Pendiente*, *Procesando*, *Completo*, o *Cancelado*.
* **Estado de pago**, como *Todo*, *Pendiente*, *Autorizado*, *Pagado*, *Reembolsado*, *Reembolsado parcialmente*, o *Anulado*.
* Elija la **Categoría**. 
* Elija el **Fabricante**.
* Elija el **País de facturación**.
* Elija el **Vendedor**.

Luego haga clic en **Run report**.

El informe desglosará sus productos más vendidos basándose en las unidades vendidas y los ingresos:

![Bestsellers](_static/reports/bestsellers.jpeg)

### Productos nunca comprados

Para ver los productos nunca comprados, vaya a **Informes → Productos nunca comprados**. Introduzca uno o más de los siguientes criterios de búsqueda para ejecutar el informe:
* Elija la **Categoría**. 
* Elija el **Fabricante**.
* **Tienda**, si desea seleccionar una de sus tiendas.
* Elija el **Vendedor**.
* **Fecha de inicio** y/o **Fecha de finalización**.

Luego haga clic en **Run report**.

![Products never purchased](_static/reports/never-purchased.jpg)


## Tutoriales

* [Running reports in nopCommerce](https://www.youtube.com/watch?v=IbfoppTG9tM)
