## 🔹 Obtención y modificación de los nodos hijos (childs)

En el modelo del DOM, los **nodos hijos** son aquellos elementos que se encuentran directamente dentro de otro nodo. Comprender cómo obtenerlos y manipularlos es fundamental para recorrer, estructurar o modificar la jerarquía del documento.  
A continuación, se detallan las propiedades y métodos más importantes relacionados con los elementos hijos.

---

### 🔸 `.children`

La propiedad `.children` devuelve una **colección viva (HTMLCollection)** que contiene **solo los nodos hijos que son elementos HTML**.  
Esto significa que no incluye nodos de texto, saltos de línea ni comentarios, concentrándose exclusivamente en los nodos de tipo `ELEMENT_NODE`.

**Ejemplo:**

```html
<ul id="lista">
  <li>Primer ítem</li>
  <li>Segundo ítem</li>
  <li>Tercer ítem</li>
</ul>

<script>
  const lista = document.getElementById("lista");
  console.log(lista.children); // HTMLCollection(3) [li, li, li]
</script>
```

**Explicación:**  
El resultado es una colección que se actualiza automáticamente si se agregan o eliminan elementos dentro de la lista. Por tanto, si luego se añade un nuevo `<li>`, aparecerá en la misma colección sin necesidad de volver a ejecutar la consulta.

---

### 🔸 `.childNodes`

La propiedad `.childNodes` devuelve **todos los nodos hijos** del elemento, incluyendo **nodos de texto, comentarios y espacios vacíos**.  
A diferencia de `.children`, esta propiedad devuelve una **NodeList**, que puede contener cualquier tipo de nodo, no solo elementos HTML.

**Ejemplo:**

```html
<div id="contenedor">
  Texto
  <p>Elemento hijo</p>
</div>

<script>
  const cont = document.getElementById("contenedor");
  console.log(cont.childNodes);
</script>
```

**Resultado:**

```
NodeList(3) [#text, p, #text]
```

**Explicación:**  
Los espacios y saltos de línea dentro del HTML también son considerados nodos de texto (`#text`).  
Por este motivo, `.childNodes` es ideal cuando se requiere acceder al documento a un nivel bajo, manipulando no solo elementos, sino también el contenido textual.

---

### 🔸 `.firstElementChild`

Devuelve el **primer hijo que sea un elemento** dentro del nodo actual.  
Si el primer hijo no es un nodo de tipo elemento (por ejemplo, si es texto), se lo omite y se retorna el primer elemento válido.  
Si el nodo no tiene hijos de tipo elemento, retorna `null`.

**Ejemplo:**

```html
<div id="bloque">
  <p>Primer párrafo</p>
  <p>Segundo párrafo</p>
</div>

<script>
  const bloque = document.getElementById("bloque");
  console.log(bloque.firstElementChild.textContent);
</script>
```

**Salida:**

```
Primer párrafo
```

**Explicación:**  
El navegador ignora los espacios o saltos de línea entre las etiquetas y devuelve directamente el primer elemento `<p>` dentro del `<div>`.

---

### 🔸 `.lastElementChild`

Devuelve el **último hijo elemento** del nodo.  
Al igual que `.firstElementChild`, ignora los nodos que no sean de tipo elemento (por ejemplo, texto o comentarios).

**Ejemplo:**

```html
<div id="bloque">
  <p>Primer párrafo</p>
  <p>Segundo párrafo</p>
</div>

<script>
  const bloque = document.getElementById("bloque");
  console.log(bloque.lastElementChild.textContent);
</script>
```

**Salida:**

```
Segundo párrafo
```

**Explicación:**  
Este método resulta útil cuando se necesita acceder directamente al último elemento dentro de un contenedor sin recorrer la lista completa.

---

### 🔸 `.firstChild` y `.lastChild`

Estas propiedades acceden al **primer y último nodo** del elemento, sin importar su tipo.  
Pueden devolver nodos de texto, comentarios o elementos, dependiendo de lo que haya en el documento.

**Ejemplo:**

```html
<div id="demo">
  Hola
  <span>Mundo</span>
</div>

<script>
  const demo = document.getElementById("demo");
  console.log(demo.firstChild);  // #text ("Hola" con espacio)
  console.log(demo.lastChild);   // #text (posible salto de línea)
</script>
```

**Explicación:**  
A diferencia de `.firstElementChild`, aquí el navegador **no filtra** el tipo de nodo, por lo que es más detallado pero también más propenso a incluir espacios o saltos no deseados.

---

## 🔹 Métodos de modificación de hijos

Una vez obtenidos los nodos hijos, el DOM permite modificarlos mediante distintos métodos.  
Estos pueden agregar, insertar, reemplazar o eliminar elementos dentro del árbol del documento.

---

### 🔸 `.appendChild()`

Agrega un nuevo nodo **al final** de la lista de hijos del elemento padre.  
Si el nodo que se agrega ya existe en otra parte del DOM, este se **mueve** a la nueva posición.

**Ejemplo:**

```html
<ul id="lista"></ul>

<script>
  const lista = document.getElementById("lista");
  const nuevo = document.createElement("li");
  nuevo.textContent = "Nuevo ítem";
  lista.appendChild(nuevo);
</script>
```

**Explicación:**  
El elemento `<li>` se crea dinámicamente y se añade al final de la lista.  
Si el `<li>` ya existía en otro contenedor, sería trasladado automáticamente.

---

### 🔸 `.insertBefore()`

Permite insertar un nodo **antes de un hijo específico** del padre.  
Este método es útil para controlar con precisión la posición del nuevo elemento dentro del contenedor.

**Ejemplo:**

```html
<ul id="lista">
  <li>Elemento 1</li>
  <li>Elemento 2</li>
</ul>

<script>
  const lista = document.getElementById("lista");
  const nuevo = document.createElement("li");
  nuevo.textContent = "Elemento 1.5";

  lista.insertBefore(nuevo, lista.children[1]);
</script>
```

**Explicación:**  
El nuevo `<li>` se inserta antes del segundo elemento de la lista.  
De esta manera, se ubica entre “Elemento 1” y “Elemento 2”.

---

### 🔸 `.removeChild()`

Elimina un nodo hijo específico del elemento padre.  
Este método requiere una referencia directa al nodo que se va a eliminar.

**Ejemplo:**

```html
<ul id="lista">
  <li>Eliminar este</li>
</ul>

<script>
  const lista = document.getElementById("lista");
  const hijo = lista.firstElementChild;
  lista.removeChild(hijo);
</script>
```

**Explicación:**  
El método elimina el `<li>` de la lista, modificando directamente la estructura del DOM.

---

### 🔸 `.replaceChild()`

Reemplaza un nodo hijo existente con un nuevo nodo.  
Esto conserva la posición original, pero cambia completamente el contenido o tipo del nodo.

**Ejemplo:**

```html
<div id="contenedor">
  <p>Texto viejo</p>
</div>

<script>
  const cont = document.getElementById("contenedor");
  const nuevo = document.createElement("h2");
  nuevo.textContent = "Texto nuevo";
  cont.replaceChild(nuevo, cont.firstElementChild);
</script>
```

**Explicación:**  
El párrafo `<p>` se reemplaza por un encabezado `<h2>`, manteniendo su ubicación dentro del contenedor.

---

### 🔸 `.replaceChildren()`

Reemplaza **todos los hijos** de un elemento con nuevos nodos, o los elimina si no se proporciona ninguno.  
Es una forma moderna y eficiente de limpiar o reconstruir el contenido interno de un contenedor.

**Ejemplo:**

```html
<div id="contenedor">
  <p>Elemento 1</p>
  <p>Elemento 2</p>
</div>

<script>
  const cont = document.getElementById("contenedor");
  cont.replaceChildren(document.createElement("span"));
</script>
```

**Explicación:**  
Ambos párrafos se eliminan y el contenedor queda con un único `<span>`.  
Si se llamara sin argumentos (`cont.replaceChildren()`), el contenedor quedaría vacío.

---

