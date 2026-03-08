#  EL OBJETO `document` Y SUS PROPIEDADES
## 1. Introducción al objeto `document`

El **objeto `document`** es uno de los objetos más importantes del entorno del navegador, ya que **representa el documento HTML cargado en la ventana actual**.  
A través de él, JavaScript puede **leer, modificar, eliminar o crear elementos** dentro de la página web.

Cuando el navegador carga una página HTML, crea una representación en memoria del documento llamada **árbol del DOM**.  
El objeto `document` es la **raíz principal** desde la cual podemos acceder a cualquier parte de ese árbol.

---

### 🏗️ Diagrama simplificado del DOM y la posición de `document`

```
WINDOW (objeto global del navegador)
│
└── document (representa el HTML cargado)
     │
     ├── <html>
     │     ├── <head>
     │     └── <body>
     │           ├── <h1>
     │           ├── <p>
     │           └── ...
```

- `window` → representa la ventana o pestaña del navegador.
    
- `document` → representa el contenido HTML dentro de esa ventana.
    
- `html`, `head` y `body` → son **nodos** del árbol del DOM a los que accedemos mediante el objeto `document`.
    

---

## 2. Naturaleza y función del objeto `document`

El objeto `document` **no se crea manualmente**: el navegador lo genera automáticamente al interpretar el HTML.  
Su función principal es **proveer una interfaz** entre el código JavaScript y la estructura HTML del documento.

Podemos considerarlo como una **“puerta de entrada”** a la manipulación del DOM.

---

### 📌 Ejemplo inicial:

Supongamos que tenemos este HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi página</title>
  </head>
  <body>
    <h1 id="titulo">Bienvenidos</h1>
    <p class="texto">Este es un párrafo.</p>
  </body>
</html>
```

Desde JavaScript, podemos acceder al contenido con `document`:

```js
console.log(document.title);       // "Mi página"
console.log(document.body);        // Devuelve el elemento <body> completo
console.log(document.getElementById("titulo")); // <h1 id="titulo">Bienvenidos</h1>
```

---

## 3. Propiedades principales del objeto `document`

A continuación se listan y explican las **propiedades más relevantes** del objeto `document`, con ejemplos y comentarios detallados.

---

### 🧩 3.1. `document.body`

Devuelve el **elemento `<body>` completo**, que contiene todo el contenido visible de la página (texto, imágenes, botones, etc.).

```js
console.log(document.body); // Muestra el nodo <body>
document.body.style.backgroundColor = "lightblue";
```

> 📘 Es una de las propiedades más utilizadas para modificar estilos o contenido globalmente.

---

### 🧩 3.2. `document.head`

Devuelve el elemento `<head>`, que incluye metadatos, enlaces a hojas de estilo, scripts y el título de la página.

```js
console.log(document.head);
```

> Suele usarse para inspeccionar o modificar el título (`<title>`) o agregar dinámicamente scripts o enlaces CSS.

---

### 🧩 3.3. `document.documentElement`

Devuelve el nodo raíz del documento, es decir, el elemento `<html>`.

```js
console.log(document.documentElement);
```

> Representa la raíz del árbol del DOM. Si queremos recorrer todo el documento desde el nodo superior, esta propiedad es clave.

---

### 🧩 3.4. `document.title`

Permite **obtener o cambiar el texto del título** que aparece en la pestaña del navegador.

```js
console.log(document.title);  // Obtiene el título actual
document.title = "Nuevo título"; // Cambia el título de la pestaña
```

---

### 🧩 3.5. `document.URL`

Devuelve la URL completa de la página cargada.

```js
console.log(document.URL);
```

> Es de solo lectura. Sirve para verificar desde qué dirección se cargó el documento.

---

### 🧩 3.6. `document.domain`

Devuelve el **dominio actual** del documento.

```js
console.log(document.domain);
```

> Ejemplo: si la página es `https://www.misitio.com/pagina.html`, devolverá `www.misitio.com`.

---

### 🧩 3.7. `document.lastModified`

Devuelve la fecha y hora de la última modificación del documento HTML.

```js
console.log(document.lastModified);
```

> Útil para mostrar información sobre actualizaciones del sitio.

---

### 🧩 3.8. `document.characterSet`

Indica la codificación de caracteres utilizada (por ejemplo `UTF-8`).

```js
console.log(document.characterSet);
```

---

### 🧩 3.9. `document.forms`, `document.images`, `document.links`

Son **colecciones vivas** (live HTMLCollections) que contienen ciertos elementos del documento:

|Propiedad|Contiene|Ejemplo|
|---|---|---|
|`document.forms`|Todos los formularios `<form>`|`console.log(document.forms[0]);`|
|`document.images`|Todas las imágenes `<img>`|`console.log(document.images.length);`|
|`document.links`|Todos los enlaces `<a>` con `href`|`console.log(document.links);`|

> “Colección viva” significa que si se agregan elementos al DOM, estas propiedades se actualizan automáticamente.

---

### 🧩 3.10. `document.readyState`

Indica el **estado de carga del documento**.  
Sus posibles valores son:

|Valor|Significado|
|---|---|
|`"loading"`|El documento aún se está cargando.|
|`"interactive"`|El documento ha sido cargado parcialmente, pero aún se están ejecutando algunos scripts.|
|`"complete"`|La página está completamente cargada.|

```js
console.log(document.readyState);
```

---

### 🧩 3.11. `document.activeElement`

Devuelve el elemento que **actualmente tiene el foco** (por ejemplo, un input o botón seleccionado).

```js
console.log(document.activeElement);
```

---

### 🧩 3.12. `document.cookie`

Permite leer o escribir cookies asociadas al documento.

```js
console.log(document.cookie);
```

> ⚠️ Manejar cookies requiere comprender aspectos de seguridad, por lo que suele tratarse en temas más avanzados.

---

### 🧩 3.13. `document.scripts`

Devuelve una colección de todos los elementos `<script>` del documento.

```js
console.log(document.scripts);
```

---

### 🧩 3.14. `document.styleSheets`

Devuelve todas las hojas de estilo asociadas al documento.

```js
console.log(document.styleSheets);
```

---

### 🧩 3.15. `document.children`

Devuelve una colección de los elementos hijos directos del documento (por lo general `<html>`).

```js
console.log(document.children);
```

---

## 4. Diferencia entre propiedades y métodos del objeto `document`

|Tipo|Ejemplo|Función principal|
|---|---|---|
|**Propiedades**|`document.body`, `document.title`|Acceden o modifican información general o nodos principales.|
|**Métodos**|`document.getElementById()`, `document.querySelector()`|Buscan, crean o eliminan nodos dentro del DOM.|

**Ejemplo combinado:**

```js
// Propiedad
document.title = "Ejemplo combinado";

// Método
let h1 = document.getElementById("titulo");
h1.textContent = "Título cambiado dinámicamente";
```

---

## 5. Diagrama conceptual: Estructura jerárquica del DOM y `document`

```
window
│
└── document
     ├── head
     │     ├── meta
     │     ├── link
     │     └── title
     │
     └── body
           ├── h1
           ├── p
           ├── div
           └── ...
```

> Cada nodo es un **objeto** dentro del árbol, y todos se pueden manipular desde `document`.

---

## 6. Conclusión

El **objeto `document`** es la **columna vertebral de la manipulación del DOM** en JavaScript.  
Permite acceder tanto a **información global** del documento (título, URL, dominio, etc.) como a **elementos específicos** mediante métodos de selección.

Comprenderlo en profundidad es esencial para avanzar hacia la **interactividad del DOM**, donde entra en juego la **manipulación dinámica de elementos** y los **eventos**.

---

¿Querés que te lo prepare también en **formato PDF bien maquetado** para tenerlo como apunte descargable (con títulos, colores, diagramas tipográficos y secciones claras)?