---
title: Manual (fixed or by weight and by total)
uid: en/getting-started/configure-shipping/shipping-providers/manual
author: git.AndreiMaz
contributors: git.rajupaladiya, git.DmitriyKulagin, git.exileDev, git.mariannk
---

# Proveedor manual (fijo o por peso y total)

El envío manual (fijo o por peso y total) permite establecer tarifas fijas o calcular las tarifas por peso y en total a todos los métodos de envío predefinidos.

Para ver el ejemplo de cómo se puede aplicar este método a su tienda, consulte la sección [Ejemplo](#example)a continuación.

# Definir el proveedor de envío manual

Ir a **Configuración > Envíos > Proveedores de envío**. Se muestra la ventana Proveedores de envío:

![métodos de envío manual](_static/manual/methods.jpg)

Habilite el método de cálculo manual de la tarifa de envío, como se indica a continuación:

* En la fila **Manual (fijo o por peso y total)**,  haga clic en el  botón Editar.
* En la columna **Está activo**,  marque la casilla de verificación.
* Haga clic en el botón **Actualizar**.  La opción *false*  se convierte en  *true*.

Haga clic en el botón Configurar  junto a la opción Manual (fijo o por peso y total) de la lista.

Puede cambiar el cálculo de la tarifa de envío *Tarifa fija* al envío *Por peso/total*  cálculo haciendo clic en el botón en la parte superior de la página.

# Configurar la tarifa fija

![Configuración manual](_static/manual/fixed-rate-configure.jpg)

Haga clic en el botón Editar junto  a un método de envío e introduzca los  días   de tránsito y  velocidad .*.

Haga clic en **Actualizar**.

> [!NOTA]
>
> Puede agregar/eliminar métodos de envío en la  *ventana Métodos de envío*, a laque se accede haciendo clic en ![ botón](_static/manual/manual-shipping-manage-button.png) y restringir algunosmétodos para los países elegidos haciendo clic en ! [restricciones](_static/manual/manual-shipping-restrictions.png) en la partesuperior.

# Configure la tasa por peso/total

![por peso](_static/manual/manual-shipping-by-weight-total.png)

La opción **envío por peso y en total**  permite establecer diferentes gastos de envío en función del peso y el total del envío. La capacidad de cobrar diferentes tarifas dependiendo del peso y el total del envío ayuda a mantener los costos de envío de la compañía hacia abajo cuando se envían artículos pesados, pero ofrecen costos de envío razonables a los clientes que compran productos ligeros.

Utilice la fórmula **[coste fijo adicional] + ([peso total del pedido] - [límite de peso inferior]) &times; [tasa por unidad de peso] + [subtotal de pedido] &times; [porcentaje de carga]**  para calcular las tasas, cuando:

* **coste fijo adicional**  - es el costo del envío en caso de que el peso esté por debajo de un cierto nivel (límite de peso más bajo).
* **tasa por unidad de peso**  - es el costo de cada unidad de peso por encima del límite de peso inferior.
* **orden de subtotal y porcentaje de cargo**  - son parámetros para calcular el costo adicional basado en el subtotal de pedido.

Por ejemplo, si tiene las siguientes condiciones de envío:

* de peso 0 a 1 libras y ordene el subtotal de $1 y ordene el subtotal a $10 el costo es de $10. Debe crear las  siguientes reglas deenvío:
* Peso del pedido de:  **0**
* Peso del pedido a:  **1**
* Subtotal de pedido de:  **1**
* Ordene el subtotal a:  **10**
* Costo fijo adicional:  **10**
* Límite de peso inferior:  **0**
* Tarifa por unidad de peso:  **0**
* desde el peso 1.1 libras a 2 libras y ordene el subtotal de $11 y ordene el subtotal a $1000000 el costo es de $15. Debe crear las  siguientes reglas deenvío:
* Peso del pedido de:  **1.000**
* Peso del pedido a:  **2**
* Subtotal de pedido de:  **11**
* Ordene el subtotal a:  **1000000**
* Costo fijo adicional:  **15**
* Límite de peso inferior:  **0**
* Tarifa por unidad de peso:  **0**
* más de 2 libras el costo es de $3 por cada 0.5 libras adicionales. Debe crear las  siguientes reglas deenvío:
* Si su costo fijo es de $15 y $6 por libras sobre 2 libras
* Peso del pedido de:  **2.0001**
* Peso del pedido a:  **99999**
* Costo fijo adicional:  **15**
* Límite de peso inferior:  **2**
* Tarifa por unidad de peso:  **3**
  
> [!NOTA]
>
> Se cobrará proporcionalmente por el peso adicional;
> ejemplo para 2.1 libras que cobrará $15 + (0.1 * 6) $ 15.6

Para agregar una nueva regla de envío, haga clic en **Agregar registro**. Se muestra la ventana *Agregar nuevo registro*:  

![Agregar regla](_static/manual/manual-shipping-add-new.jpg)

Defina la siguiente información:

* **Tienda**  en la que se aplicarán las tarifas calculadas. Elija * para aplicar las reglas a todas las tiendas.
* **Almacén**  desde el que se realizará el envío. Elija * para aplicar las reglas a todos los almacenes.
* **País, Estado/provincia, Zip**  de un destino de envío.
* Seleccione un método de envío *** de la lista de opciones creadas previamente. Utilice  **Administrar métodos de envío**  en la parte superior para agregar o quitar métodos de envío.
* Crea tu configuración de peso llenando los campos **Order weight from**  y  **Order weight to**.  Si el peso de envío del cliente cae en este rango, el costo adicional se fijará y se calculará de acuerdo con este registro.
* Configure las reglas de precios para este registro usando los campos  **Ordenar subtotal de, Ordenar subtotal a, Coste fijo adicional, Límite de peso más bajo, Tasa por unidad de peso, Porcentaje de cargo (de subtotal)**campos.  
* Defina el campo **Días de tránsito**  que define el número de días de entrega.

> [!NOTA]
>
> Asegúrese de que la configuración  **Configuración > Configuración > Ajustes de envío > Considere las dimensiones y el peso de los productos asociados**  es verdadera.

Haga clic en **Guardar**.

> [!NOTA]
>
> Si desea limitar a sus clientes solo a los métodos configurados en esa pantalla, marque la casilla **Limitar los métodos de envío a los configurados**  en la parte inferior de la página.

# Configurar métodos de envío

El propietario de una tienda puede definir la lista de métodos de envío requeridos que se utiliza en el proveedor *Manual (fijo o por peso y total)*.  Para gestionar los métodos de envío:

Ir a **Configuración > Envíos > Proveedores de envío**. A continuación, haga clic en el  botón  Configurar junto al proveedor *Manual (fijo o por peso y total)*.  Se visualiza la ventana de configuración:

![Configurar](_static/manual/fixed-rate-configure.jpg)

Haga clic en **Administrar métodos de envío**, se muestra la ventana *Métodos de envío*:  

![Métodos](_static/manual/fixed-rate-methods.jpg)

Haga clic en el botón Agregar nuevo, se muestra la ventana *Agregar un nuevo método de envío*,  como se indica a continuación:

![Añadir nuevo](_static/manual/fixed-rate-methods-add-new.jpg)

Defina los campos siguientes para un nuevo registro:

* **Nombre**  del método de envío visto por un cliente.
* **Descripción**  para el método de envío visto por un cliente.
* **Mostrar pedido**  del método de envío. Un valor de 1 representa la parte superior de la lista.

Haga clic en **Guardar**.

> [!NOTA]
>
> Puede hacer clic en Editar en la ventana *Métodos de envío* para editar los  métodos de envío existentes, como se describió anteriormente.

# Restricciones del método de envío

El propietario de una tienda puede definir restricciones para ciertos métodos de envío en determinados países. Para ello, vaya a **Configuración > Envío > Proveedores de envío**. Haga clic en el  botón  **Configurar** situado junto al proveedor *Manual (fijo o por peso y total)*.  Se visualiza la ventana de configuración:

![Configurar](_static/manual/fixed-rate-configure.jpg)

Haga clic en **Restricciones del método de envío**, se muestra la ventana *Restricciones del método de envío*:  

![Métodos](_static/manual/fixed-rate-restrictions-methods.jpg)

Seleccione uno o varios de sus métodos de envío que desea deshabilitar en ciertos países.

Si es necesario, puede seleccionar toda la columna de restricción para todos los países.

Haga clic en **Guardar**.

# Ejemplo

Ley dice que tienes una tienda ubicada en los EE.UU. y envía a los EE.UU. y Canadá. Puede configurar tres métodos de envío disponibles, como:
- **Tierra**  que permite el envío por transporte terrestre.
- **Aire al día siguiente**  que proporciona envío aéreo de un día.
- **2o día de aire**  permitiendo dos días de envío aéreo.

> [!CONSEJO]
>
> Puede agregar sus propios métodos de envío haciendo clic en el  botón  **Administrar métodos de envío** en la página *Configurar - Manual (Fijo o Por peso y Por total)*.  

A continuación, supongamos que la tarifa de envío depende del total del pedido y de la dirección de envío. Por ejemplo:
- Si un cliente paga $150 por el pedido, proporcionamos un envío gratuito por el método **Ground** solo a EE. UU. Si el total del pedido es inferior a $150, cobraremos $10. La entrega a los EE.UU. tomará 5 días.
- Para Canadá, un cliente debe pedir $250 para tener un envío gratuito por el método **Ground**.  Si el total del pedido es inferior a $250, cobraremos $20. La entrega en este caso tomará 7 días.
- Si un cliente necesita una entrega de aire al día siguiente**  costará $60 para los EE.UU. Supongamos que desea desactivar la opción de aire al día siguiente  para Canadá.
- Si un cliente está listo para esperar un día más, le sugerimos que utilice el envío aéreo del segundo día del segundo día,  que cuesta $40 para los EE.UU. y Canadá también.

Teniendo en cuenta todos los requisitos anteriores, configuraremos el método de pago en la página *Configurar - Manual (Fijo o Por Peso y Por Total)*  de la siguiente manera:

- **Método de tierra**  
![Tierra de configuración](_static/manual/configuration-ground.jpg)

- **Aire al día siguiente**  método
![Configuración Aire al día siguiente](_static/manual/configuration-nextday.jpg)

- **2o día de aire**  método
![Configuración 2nd day air](_static/manual/configuration-2ndday.jpg)

Para desactivar la opción de aire al día siguiente para Canadá, haga clic en el  botón  **Restricciones del método de envío** y rellene las restricciones del método *Envío*  de la siguiente manera:
![Ejemplo de configuración](_static/manual/restrictions-example.jpg)

# Veamos cómo se ven las opciones de envío en la tienda pública

1. Cuando un cliente de EE. UU. visita la página del producto (o página del carro de la compra), se muestra la estimación de envío, como se muestra a continuación:
![Estimación](_static/manual/estimate-product-page.jpg)
> [!CONSEJO]
>
> Por cierto, puede desactivar la estimación de envío desmarcando las casillas de verificación  **Estimar envío habilitado (página de carrito)**  y  **Estimar el envío habilitado (página del producto)** en la página **Configuración > Configuración > Configuración de envío**.  

Cuando el cliente proceda a los detalles de envío, se mostrarán las siguientes opciones:
![Estimación EE.UU.](_static/manual/estimation-popup-usa.jpg)

2. Cuando un cliente elige Canadá en la ventana de estimación de envío, se mostrarán las siguientes opciones:
![Estimación Canadá](_static/manual/estimación-popup-canada.jpg)
Como puede ver, la opción **Aire al día siguiente**  ya no está disponible.

> [!CONSEJO]
>
> En caso de que desee proporcionar puntos de recogida a sus clientes ver cómo configurar esto en el[ Puntos derecogida](xref:en/getting-started/configure-shipping/advanced-configuration/pickup-points)capítulo.

# Tutoriales

* [Configuración del método de envío manual](https://www.youtube.com/watch?v=1nYj0NqVUWw&t=8s)


