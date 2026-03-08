## 📘 **Los Nodos del DOM: Tipos, Propiedades y Relaciones**

---

### 🧩 **1. Qué es un nodo**

En el contexto del DOM, un **nodo** es **cada unidad individual que forma parte del árbol del documento**.  
Todo lo que existe en el documento HTML —etiquetas, texto, atributos, comentarios, etc.— se traduce internamente a **nodos** que se organizan jerárquicamente.

> 🔹 En términos simples: un **nodo es un objeto que representa una parte del documento**.

---

### 🌳 **2. Tipos de nodos en el DOM**

El DOM define **12 tipos de nodos**, aunque en la práctica se usan principalmente los más comunes (Element, Text, Comment, Document, DocumentFragment y Attribute).

A continuación te dejo una lista completa con su descripción, constante numérica, ejemplos y comportamiento:

|Tipo de Nodo|Constante|Descripción|Ejemplo HTML|Representación DOM|Observaciones|
|---|---|---|---|---|---|
|**1 – ELEMENT_NODE**|`Node.ELEMENT_NODE`|Representa cualquier **elemento HTML o XML**.|`<div></div>`|`div`|Es el más común. Permite acceder a sus atributos, hijos, etc.|
|**2 – ATTRIBUTE_NODE**|`Node.ATTRIBUTE_NODE`|Representa un **atributo** de un elemento.|`<img src="foto.png">`|`src="foto.png"`|En DOM moderno se accede vía propiedades (`.getAttribute()`, `.setAttribute()`), no directamente como nodo.|
|**3 – TEXT_NODE**|`Node.TEXT_NODE`|Representa el **contenido textual** de una etiqueta.|`<p>Hola</p>`|`"Hola"`|Puede incluir espacios, saltos de línea, etc.|
|**4 – CDATA_SECTION_NODE**|`Node.CDATA_SECTION_NODE`|Se usa en documentos XML para texto sin interpretar.|`<![CDATA[ texto sin parsear ]]>`|—|No se usa en HTML, solo en XML.|
|**5 – ENTITY_REFERENCE_NODE**|`Node.ENTITY_REFERENCE_NODE`|Nodo para referencias a entidades en XML.|`&amp;`|—|Obsoleto.|
|**6 – ENTITY_NODE**|`Node.ENTITY_NODE`|Define una entidad en un DTD (Document Type Definition).|—|—|Usado en XML. Obsoleto.|
|**7 – PROCESSING_INSTRUCTION_NODE**|`Node.PROCESSING_INSTRUCTION_NODE`|Instrucciones para procesadores XML.|`<?xml-stylesheet ... ?>`|—|No se usa en HTML.|
|**8 – COMMENT_NODE**|`Node.COMMENT_NODE`|Representa los **comentarios** del HTML.|`<!-- comentario -->`|`#comment`|No se muestra visualmente.|
|**9 – DOCUMENT_NODE**|`Node.DOCUMENT_NODE`|Representa el **documento completo**.|`document`|`#document`|Es el nodo raíz. En JavaScript se accede como `document`.|
|**10 – DOCUMENT_TYPE_NODE**|`Node.DOCUMENT_TYPE_NODE`|Representa el `<!DOCTYPE html>` inicial.|`<!DOCTYPE html>`|`#doctype`|Ayuda al navegador a definir el modo de renderizado.|
|**11 – DOCUMENT_FRAGMENT_NODE**|`Node.DOCUMENT_FRAGMENT_NODE`|Nodo contenedor **temporal** para manipular varios nodos antes de insertarlos.|—|`DocumentFragment`|Mejora el rendimiento en inserciones.|
|**12 – NOTATION_NODE**|`Node.NOTATION_NODE`|Define notaciones en XML.|—|—|No se usa en HTML.|

---

### ⚙️ **3. Propiedades comunes de los nodos**

Todos los nodos comparten un conjunto base de propiedades definidas por la interfaz `Node`.  
Estas permiten **identificarlos, recorrerlos y manipular su estructura**.

|Propiedad|Descripción|Ejemplo|
|---|---|---|
|`.nodeName`|Devuelve el nombre del nodo (por ejemplo, `"DIV"` o `"#text"`).|`element.nodeName` → `"P"`|
|`.nodeType`|Devuelve un número que indica el tipo de nodo (según la tabla anterior).|`element.nodeType` → `1`|
|`.nodeValue`|Devuelve o establece el valor del nodo (por ejemplo, el texto de un nodo de texto).|`textNode.nodeValue` → `"Hola"`|
|`.parentNode`|Devuelve el nodo padre.|`p.parentNode` → `body`|
|`.childNodes`|Devuelve una lista (NodeList) con todos los nodos hijos.|`body.childNodes`|
|`.firstChild` / `.lastChild`|Devuelven el primer o último hijo del nodo.|`div.firstChild`|
|`.nextSibling` / `.previousSibling`|Devuelven el siguiente o anterior nodo en el mismo nivel.|`p.nextSibling`|
|`.textContent`|Devuelve todo el texto contenido (sin etiquetas).|`div.textContent`|
|`.ownerDocument`|Devuelve el documento principal del nodo.|`element.ownerDocument` → `document`|

> 🧠 Importante: muchas de estas propiedades son dinámicas; es decir, **si el DOM cambia, sus valores cambian automáticamente.**

---

### 🔁 **4. Relaciones entre nodos**

El DOM no solo define tipos de nodos, sino también cómo se **relacionan entre sí** dentro del árbol jerárquico.  
Podemos describirlo con los siguientes términos:

|Relación|Descripción|Ejemplo|
|---|---|---|
|**Padre (parent)**|Nodo que contiene a otros nodos.|`<body>` es padre de `<div>`.|
|**Hijo (child)**|Nodo contenido dentro de otro.|`<div>` es hijo de `<body>`.|
|**Hermano (sibling)**|Nodos que comparten el mismo padre.|`<p>` y `<h1>` dentro del mismo `<div>`.|
|**Ancestro (ancestor)**|Nodo que está en la cadena de padres de otro.|`<html>` es ancestro de todos.|
|**Descendiente (descendant)**|Nodo que se encuentra dentro de otro (en cualquier nivel).|`<p>` es descendiente de `<html>`.|

---

### 🧱 **5. Representación visual: jerarquía de nodos**

Veamos un ejemplo HTML simple:

```html
<body>
  <div id="contenedor">
    <h1>Título</h1>
    <p>Texto <strong>importante</strong></p>
  </div>
</body>
```

El árbol DOM correspondiente sería:

```
body (ELEMENT_NODE)
└── div#contenedor (ELEMENT_NODE)
     ├── h1 (ELEMENT_NODE)
     │     └── "Título" (TEXT_NODE)
     └── p (ELEMENT_NODE)
          ├── "Texto " (TEXT_NODE)
          └── strong (ELEMENT_NODE)
               └── "importante" (TEXT_NODE)
```

Y sus relaciones se pueden describir así:

- `body` es padre de `div`.
    
- `div` es padre de `h1` y `p`.
    
- `h1` y `p` son hermanos.
    
- `strong` es hijo de `p` y nieto de `div`.
    

---

### 💡 **6. Listas de nodos: NodeList y HTMLCollection**

Cuando obtenemos varios nodos mediante métodos del DOM, estos se almacenan en **colecciones**.  
Las dos más comunes son:

#### 🔸 NodeList

- Devuelta por métodos como `.childNodes`, `querySelectorAll()`.
    
- Puede contener cualquier tipo de nodo (elementos, textos, comentarios).
    
- Puede ser **estática o viva**:
    
    - Estática: no se actualiza si el DOM cambia (como `querySelectorAll()`).
        
    - Viva: se actualiza automáticamente (como `.childNodes` en algunos casos).
        

#### 🔸 HTMLCollection

- Devuelta por métodos como `.children`, `.getElementsByTagName()`, `.getElementsByClassName()`.
    
- Contiene **solo elementos HTML** (sin textos ni comentarios).
    
- Siempre es **viva** (se actualiza si el DOM cambia).
    

Ejemplo:

```js
let div = document.querySelector("#contenedor");
console.log(div.childNodes);   // NodeList (incluye texto)
console.log(div.children);     // HTMLCollection (solo elementos)
```

---

### ⚡ **7. Resumen conceptual**

|Concepto|DOM|Nodos|Render Tree|
|---|---|---|---|
|Qué es|Representación lógica del documento|Unidades del DOM|Estructura visual derivada del DOM + CSSOM|
|Función|Permite manipular y recorrer el documento|Construyen el DOM|Controlan el renderizado visual|
|Tipos|1 por documento|12 tipos|Solo visibles|
|Ejemplo|`<body><p>Hola</p></body>`|Element, Text, Comment|`<p>Hola</p>` visible|

---
