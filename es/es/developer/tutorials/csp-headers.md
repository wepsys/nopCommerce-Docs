---
title: Content Security Policy (CSP) Headers
uid: en/developer/tutorials/csp-headers
author: git.nopsg
contributors: git.nopsg, git.DmitriyKulagin
---

# Encabezados de la política de seguridad de contenido (CSP)

Content-Security-Policy es el nombre de un encabezado de respuesta HTTP que los navegadores modernos utilizan para mejorar la seguridad del documento (o página web). El encabezado de respuesta de la Política de seguridad de contenido HTTP les da a los administradores de sitios web una sensación de control al darles la autoridad para restringir los recursos como JavaScript y CSS que un usuario puede cargar dentro del sitio. En otras palabras, puede incluir en la lista blanca las fuentes de contenido de su sitio. Aunque se usa principalmente como encabezado de respuesta HTTP, también puede aplicarlo a través de una metaetiqueta.

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src 'self' https://img.nopcommerce.com; object-src 'none'; script-src 'self'; style-src 'self'; frame-ancestors 'self'; base-uri 'self'; form-action 'self';">
```

Para agregar esta metaetiqueta personalizada, puede ir a `www.yourStore.com/Admin/Setting/GeneralCommon` y encontrar **`Custom <head> tag`** and add this as shown in image below.

![imagen de etiqueta de cabeza CSP personalizada](_static/csp-headers/custom-csp-head-tag.png)

La política de seguridad de contenido protege contra **Cross Site Scripting (XSS)** y otras formas de ataques como **Click Jacking**. Aunque no elimina por completo su posibilidad, seguramente puede minimizar el daño. La compatibilidad no es un problema, ya que la mayoría de los principales navegadores admiten CSP. No es compatible con Internet Explorer.

Para probar su navegador si es compatible con CSP o no, puede seguir esto [link](https://content-security-policy.com/browser-test/).

## Default CSP (Referencia de la directiva CSP)

El valor del encabezado ** Content-Security-Policy ** se compone de una o más directivas (definidas a continuación), las directivas múltiples se separan con un * punto y coma (;) *

### default-src (directivas-src) 

La directiva *default-src* define la política predeterminada para obtener recursos como JavaScript, imágenes, CSS, fuentes, solicitudes AJAX, marcos, HTML5 Media. No todas las directivas recurren a *default-src*.

```html
default-src 'self' cdn.nopcommerce.com;
```

### script-src

Define fuentes válidas de JavaScriptt.

```html
script-src 'self' js.nopcommerce.com;
```

### style-src

Define fuentes válidas de hojas de estilo o CSS.

```html
style-src 'self' css.nopcommerce.com;
```

### img-src

Define fuentes válidas de imágenes.

```html
img-src 'self' img.nopcommerce.com;
```

### connect-src

Se aplica a *XMLHttpRequest (AJAX), WebSocket o EventSource*. Si no está permitido, el navegador emula un código de estado HTTP **400**.

```html
connect-src 'self';
```

### font-src

Define fuentes válidas de recursos de fuentes (cargadas a través de *@ font-face*).

```html
font-src font.nopcommerce.com;
```

### object-src

Define fuentes válidas o plugins, por ejemplo `<object>`, `<embed>` o `<applet>`.

```html
object-src 'self';
```

### media-src

Define fuentes válidas de audio y video, p. Ej. HTML5 `<audio>`, `<video>` elementos.

```html
media-src media.nopcommerce.com;
```

### frame-src

Define fuentes válidas para cargar marcos.

```html
frame-src 'self';
```

### sandbox

Habilita una caja de arena para el recurso solicitado similar al atributo *iframe sandbox*. El sandbox aplica una misma política de origen, evita ventanas emergentes, complementos y se bloquea la ejecución del script. Puede mantener el valor de la zona de pruebas vacío para mantener todas las restricciones en su lugar, o agregar valores: * allow-forms allow-same-origin allow-scripts allow-popups, allow-modals, allow-Orientation-lock, allow-pointer-lock, allow-presentation, allow-popups-to-escape-sandbox, *y* allow-top-navigation *

```html
sandbox allow-forms allow-scripts;
```

### child-src

Defines valid sources for web workers and nested browsing contexts loaded using elements such as `<frame>` and `<iframe>`

```html
child-src 'self'
```

### form-action

Defines valid sources that can be used as an HTML `<form>` action.

```html
form-action 'self';
```

### frame-ancestors (marco-ancestros)

Define fuentes válidas para trabajadores web y contextos de navegación anidados cargados con elementos como `<frame> <iframe> <object> <embed> <applet>`. Establecer esta directiva en ** 'none' ** debería ser aproximadamente equivalente a **X-Frame-Options: DENY**

```html
frame-ancestors 'none';
```

### plugin-types (tipos de complementos)

Define tipos MIME válidos para complementos invocados a través de `<object>` Y`<embed>`. Para cargar un `<applet>` debes especificar *application/x-java-applet*.

```html
plugin-types application/pdf;
```

### Reportar a

Define un nombre de grupo de informes definido por un encabezado de respuesta HTTP *Report-To*. Ver el [Reporting API](https://w3c.github.io/reporting/) para más información.

```html
report-to groupName;
```

### worker-src

Restringe las URL que se pueden cargar como Worker, SharedWorker o ServiceWorker.

```html
worker-src 'none';
```

### manifest-src

Restringe las URL en las que se pueden cargar los manifiestos de la aplicación.

```html
manifest-src 'none';
```

### navigate-to

Restringe las URL a las que puede navegar el documento por cualquier medio. Por ejemplo, cuando se hace clic en un enlace, se envía un formulario o se invoca *window.location*. Si *form-action* está presente, esta directiva se ignora para los envíos de formularios. [Implementation Status](https://www.chromestatus.com/features/6457580339593216)

```html
navigate-to nopcommerce.com
```

## Ejemplos de políticas de seguridad de contenido

### Permitir todo pero solo desde el mismo origen

```html
default-src 'self';
```

### Permitir solo scripts del mismo origen

```html
script-src 'self';
```

### Permitir Google Analytics, Google AJAX CDN y Same Origin

```html
script-src 'self' www.google-analytics.com ajax.googleapis.com;
```

### Política de inicio

```html
default-src 'none'; script-src 'self'; connect-src 'self'; img-src 'self'; style-src 'self';
```

Esta política permite imágenes, scripts, AJAX y CSS del mismo origen y no permite que se carguen otros recursos (por ejemplo, objetos, marcos, medios, etc.). Es un buen punto de partida para muchos sitios.

## Mensajes de error de política de seguridad de contenido

Según el navegador, los mensajes de error de CSP pueden diferir.

En las herramientas de desarrollo de Chrome, podemos ver el siguiente mensaje.

```js
Refused to load the script 'script-uri' because it violates the following Content Security Policy directive: "your CSP directive".
```

En las herramientas de desarrollo de Firefox de la siguiente manera.

```js
Content Security Policy: A violation occurred for a report-only CSP policy ("An attempt to execute inline scripts has been blocked"). The behavior was allowed, and a CSP report was sent.
```

Además de un mensaje de consola, se dispara un evento **securitypolicyviolation** en la ventana. Para obtener más información, siga este [link](https://www.w3.org/TR/CSP2/#firing-securitypolicyviolationevent-events.).
