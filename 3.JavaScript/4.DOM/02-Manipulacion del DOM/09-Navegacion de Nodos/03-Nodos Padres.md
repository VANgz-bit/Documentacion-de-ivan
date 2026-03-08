## 🔹 Propiedades de los elementos padres (Parents)

### 🔸 Introducción

En el árbol del DOM, cada nodo —excepto el nodo raíz (`document`)— **posee un nodo padre** del cual depende jerárquicamente.  
El padre es aquel nodo que **contiene directamente** al elemento en cuestión. Comprender cómo acceder a él y manipularlo permite recorrer el DOM desde los elementos hijos hacia niveles superiores, algo esencial para la navegación estructurada y la modificación dinámica de la página.

Por ejemplo, si un nodo `<li>` está dentro de un `<ul>`, el `<ul>` será su padre directo.  
El DOM proporciona propiedades que permiten acceder a este nodo contenedor, e incluso distinguir si el padre es un nodo de tipo elemento o cualquier tipo de nodo.

---

### 🔸 `.parentNode`

La propiedad `.parentNode` devuelve **el nodo padre inmediato** del elemento actual, sin importar su tipo.  
Esto incluye no solo elementos HTML, sino también otros tipos de nodos, como `Document` o `DocumentFragment`.

**Ejemplo:**

```html
<div id="contenedor">
  <p id="parrafo">Texto dentro del párrafo</p>
</div>

<script>
  const parrafo = document.getElementById("parrafo");
  console.log(parrafo.parentNode);
</script>
```

**Salida:**

```
<div id="contenedor">…</div>
```

**Explicación detallada:**  
El párrafo tiene como padre directo al `<div>`.  
Sin embargo, si ese `<div>` estuviera dentro de otro elemento, `parentNode` permitiría continuar ascendiendo en el árbol repitiendo la propiedad, por ejemplo:  
`parrafo.parentNode.parentNode`, y así sucesivamente, hasta llegar al nodo raíz `document`.

Esta propiedad es **muy general**, por lo que puede devolver cualquier tipo de nodo padre (no necesariamente un elemento HTML).  
Por ejemplo, el propio `<html>` tiene como padre al nodo `#document`, que representa el documento completo.

---

### 🔸 `.parentElement`

La propiedad `.parentElement` devuelve **el nodo padre si y solo si es un elemento HTML**.  
Si el nodo padre no es de tipo elemento (por ejemplo, si se trata de un `Document` o un `DocumentFragment`), la propiedad devolverá `null`.

**Ejemplo:**

```html
<section>
  <div>
    <p id="texto">Hola mundo</p>
  </div>
</section>

<script>
  const texto = document.getElementById("texto");
  console.log(texto.parentElement); // <div>…</div>
  console.log(texto.parentElement.parentElement); // <section>…</section>
</script>
```

**Explicación:**  
A diferencia de `.parentNode`, aquí el acceso está restringido a nodos que sean **Element**, es decir, elementos válidos del documento HTML.  
Esto evita encontrarse con nodos de tipo `#document`, lo que resulta útil cuando se desea trabajar exclusivamente dentro del nivel de elementos del DOM.

**Diferencia entre `.parentNode` y `.parentElement`:**

Aunque suelen coincidir en la mayoría de los casos, la distinción se vuelve importante en contextos más técnicos, como cuando se manipulan fragmentos del DOM en memoria antes de insertarlos en el documento principal.  
En esos casos, `.parentNode` puede devolver un `DocumentFragment`, mientras que `.parentElement` devolvería `null`.

---

### 🔸 Accediendo al padre del documento (`document`)

El nodo raíz `document` representa el punto más alto del árbol del DOM.  
Al ser la raíz, **no posee un padre**, por lo que tanto `document.parentNode` como `document.parentElement` devuelven `null`.

**Ejemplo:**

```js
console.log(document.parentNode);    // null
console.log(document.parentElement); // null
```

**Explicación:**  
Esto refleja que `document` es el nodo principal del árbol, el origen de toda la jerarquía de nodos.

---

### 🔸 Aplicación práctica: recorrer hacia arriba

Estas propiedades permiten recorrer el árbol del DOM desde cualquier nodo hacia sus antecesores.  
Por ejemplo, se puede verificar si un elemento pertenece a una sección o contenedor específico:

**Ejemplo:**

```html
<section id="bloque">
  <div>
    <p id="frase">Contenido dinámico</p>
  </div>
</section>

<script>
  const frase = document.getElementById("frase");
  let nodoActual = frase;

  while (nodoActual) {
    console.log(nodoActual.nodeName);
    nodoActual = nodoActual.parentElement;
  }
</script>
```

**Salida:**

```
P
DIV
SECTION
BODY
HTML
```

**Explicación:**  
El bucle asciende por toda la jerarquía hasta llegar a la raíz del documento.  
Este enfoque es útil cuando se necesita conocer la estructura superior o aplicar cambios de estilo o comportamiento basados en la jerarquía de contención.

---
