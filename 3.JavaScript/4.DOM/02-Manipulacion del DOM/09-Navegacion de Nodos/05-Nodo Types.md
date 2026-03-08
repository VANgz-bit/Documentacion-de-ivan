## ⚙️ Propiedad `nodeType`

La propiedad `nodeType` forma parte del prototipo **`Node`**, del cual heredan todos los objetos que representan nodos en el DOM.  
Su función es **identificar el tipo de nodo** con un número constante definido por la especificación del DOM.  
Cada tipo de nodo devuelve un valor distinto que permite distinguir, por ejemplo, si estamos trabajando con una etiqueta HTML, un texto o un comentario.

Cuando se ejecuta sobre un nodo, `nodeType` devuelve un número entero:

```js
console.log(document.nodeType); // 9 → DOCUMENT_NODE
```

Estos valores no son arbitrarios: están definidos en la especificación W3C y son constantes universales.

Los más importantes son:

- **1** → Elemento HTML (`ELEMENT_NODE`)
    
- **3** → Nodo de texto (`TEXT_NODE`)
    
- **8** → Comentario (`COMMENT_NODE`)
    
- **9** → Documento (`DOCUMENT_NODE`)
    
- **11** → Fragmento (`DOCUMENT_FRAGMENT_NODE`)
    

---

### 🔍 Ejemplo práctico

Imaginemos este fragmento de HTML:

```html
<div id="box">
  Texto dentro del div
  <!-- Comentario -->
</div>
```

Y el siguiente código JavaScript:

```js
const box = document.getElementById("box");

console.log(box.nodeType);            // 1 → ELEMENT_NODE
console.log(box.firstChild.nodeType); // 3 → TEXT_NODE
console.log(box.lastChild.nodeType);  // 8 → COMMENT_NODE
```

Este ejemplo demuestra cómo `nodeType` permite identificar la **naturaleza del nodo**, incluso cuando no es visible en pantalla.

---

### 🧠 Utilidad práctica

Saber el tipo de nodo es especialmente útil cuando se recorren elementos con propiedades como `childNodes`, que devuelven **todos** los nodos hijos, incluidos los de texto y los comentarios.  
En esos casos, `nodeType` permite filtrar cuáles son realmente **elementos HTML válidos** antes de manipularlos.

Por ejemplo:

```js
box.childNodes.forEach(node => {
  if (node.nodeType === 1) { // Solo elementos HTML
    console.log("Etiqueta:", node.tagName);
  }
});
```

Esto evita errores comunes al intentar aplicar propiedades o métodos de elementos sobre nodos de texto o comentarios.

---

