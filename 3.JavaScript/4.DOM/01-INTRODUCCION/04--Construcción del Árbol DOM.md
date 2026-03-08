## ⚙️ **Construcción del Árbol DOM: cómo el navegador crea la estructura interna**

---

### 🧠 **1. El objetivo del proceso**

El navegador recibe un archivo HTML como texto plano.  
Antes de poder mostrar algo en pantalla, debe **interpretar ese texto y transformarlo en una estructura de objetos**, el **árbol DOM**, que sea entendible por su motor de renderizado.

Este proceso se llama **parsing del HTML** (análisis sintáctico), y se realiza en **varias etapas secuenciales y dependientes**.

---

### 🔍 **2. Etapas del proceso de construcción**

El proceso general se puede dividir en **cinco etapas principales**:

```
1. Recepción del HTML → 
2. Tokenización → 
3. Creación de nodos → 
4. Construcción del árbol DOM →
5. Enlazado con el CSSOM (para formar el Render Tree)
```

Vamos paso a paso 👇

---

### 📥 **Etapa 1: Recepción del HTML**

El navegador comienza a **descargar el archivo HTML** desde el servidor (o desde el cache local).  
A medida que los datos llegan, el motor de renderizado **no espera a tener todo el archivo**: empieza a procesarlo **en streaming**, línea por línea, carácter por carácter.

Esto significa que **el DOM empieza a construirse antes de que el HTML termine de cargarse**.

---

### 🧩 **Etapa 2: Tokenización**

El motor HTML convierte el texto en **tokens**, es decir, en **fragmentos reconocibles del lenguaje HTML**.

Por ejemplo, el texto:

```html
<p class="saludo">Hola Mundo</p>
```

se convierte en una secuencia de tokens como:

```
StartTag: <p>
Attribute: class="saludo"
Text: "Hola Mundo"
EndTag: </p>
```

Cada token identifica **qué tipo de contenido se está procesando** (inicio de etiqueta, cierre, texto, comentario, etc.).

---

### 🧱 **Etapa 3: Creación de nodos**

Una vez que el parser identifica los tokens, los convierte en **nodos del DOM**.

Por ejemplo:

|Token|Nodo generado|Tipo|
|---|---|---|
|`<p>`|`p`|ELEMENT_NODE|
|`class="saludo"`|atributo dentro del nodo `p`|ATTRIBUTE_NODE|
|`"Hola Mundo"`|`"Hola Mundo"`|TEXT_NODE|
|`</p>`|cierra el nodo `p`|—|

En este punto, cada etiqueta o contenido textual se traduce a un **objeto en memoria**.

---

### 🌳 **Etapa 4: Construcción del Árbol DOM**

Los nodos generados se **organizan jerárquicamente** según su posición en el HTML.  
Cada nodo hijo se **inserta dentro de su nodo padre**, formando la estructura completa del árbol DOM.

Por ejemplo, a partir del siguiente HTML:

```html
<html>
  <body>
    <p>Hola Mundo</p>
  </body>
</html>
```

El navegador genera internamente esta estructura:

```
Document
└── html
     └── body
          └── p
               └── "Hola Mundo"
```

Cada relación (padre → hijo) se establece **en tiempo real mientras el HTML se parsea**.

---

### 🎨 **Etapa 5: Enlazado con el CSSOM**

Una vez que el DOM está en construcción (y el navegador encuentra etiquetas `<style>` o `<link>`), se inicia en paralelo la creación del **CSSOM** (CSS Object Model).

El **CSSOM** es un árbol que representa todas las reglas CSS aplicables a cada nodo.  
Luego, el navegador **combina el DOM + CSSOM** para generar el **Render Tree**, el cual usa para **calcular el layout y pintar la página**.

Diagrama simplificado:

```
HTML → DOM Tree
CSS  → CSSOM Tree
             ↓
     DOM + CSSOM
             ↓
       Render Tree
             ↓
        Layout + Paint
```

---

### ⏱️ **6. Orden de ejecución y bloqueos**

Durante este proceso, pueden aparecer **bloqueos temporales**, sobre todo por la carga de **scripts o estilos**.

Por ejemplo:

- Si el navegador encuentra un `<script>` **sin atributo `defer` ni `async`**, **detiene la construcción del DOM** hasta que el script se descargue y ejecute.
    
- Si encuentra un `<link>` o `<style>`, **puede esperar** a que se apliquen los estilos antes de continuar con el renderizado.
    

Esto explica por qué a veces necesitamos ejecutar JavaScript **después de que el DOM esté completamente cargado**, usando eventos como:

```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("El DOM está listo para manipularse");
});
```

---

### 🧩 **7. Ejemplo completo del proceso**

Dado el siguiente HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Ejemplo DOM</title>
  </head>
  <body>
    <h1>Hola Mundo</h1>
    <p>Bienvenido al DOM</p>
  </body>
</html>
```

El navegador realiza internamente:

|Fase|Acción|Resultado|
|---|---|---|
|**Tokenización**|Detecta etiquetas y texto.|`<html>`, `<head>`, `<body>`, `<h1>`, `<p>`|
|**Creación de nodos**|Crea objetos tipo `Element` y `Text`.|`html`, `head`, `body`, `h1`, `p`, `"Hola Mundo"`, `"Bienvenido al DOM"`|
|**Construcción jerárquica**|Asocia relaciones padre/hijo.|`body → h1 → "Hola Mundo"`|
|**Render Tree**|Une el DOM y CSSOM (si hay estilos).|Se genera la versión visual.|
|**Pintado final**|Calcula posiciones y muestra en pantalla.|Página visible al usuario.|

---

### 🔄 **8. DOM dinámico: el documento no es estático**

Una vez creado, el DOM **no queda congelado**.  
Podemos modificarlo en tiempo real con JavaScript usando métodos como:

- `document.createElement()`
    
- `appendChild()`
    
- `removeChild()`
    
- `setAttribute()`
    
- `innerHTML`
    

Cada vez que el DOM cambia:

- El navegador puede **recalcular parte del árbol**.
    
- Y dependiendo del cambio, **volver a repintar (repaint)** o **recalcular el layout (reflow)**.
    

---

### 💡 **9. En resumen**

|Etapa|Acción|Resultado|
|---|---|---|
|1️⃣ Lectura del HTML|El navegador lee el archivo.|Texto plano.|
|2️⃣ Tokenización|Se identifican las etiquetas.|Tokens.|
|3️⃣ Creación de nodos|Se generan objetos DOM.|Nodos en memoria.|
|4️⃣ Construcción del árbol|Se conectan padre e hijos.|Árbol DOM.|
|5️⃣ CSSOM + Render Tree|Se aplican estilos y se renderiza.|Visualización.|

---
