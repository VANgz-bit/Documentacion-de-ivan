## ⚙️ Método `closest()`

El método `closest()` pertenece también al conjunto de herramientas del DOM para la **navegación estructural**, pero en sentido **ascendente**:  
mientras que `parentElement` o `parentNode` devuelven el nodo padre inmediato, `closest()` busca hacia arriba en el árbol **hasta encontrar el ancestro más cercano que cumpla una condición**.

Su sintaxis es:

```js
element.closest(selector)
```

Donde `selector` es una cadena que representa un selector CSS.  
El método devuelve el **primer ancestro (incluido el propio elemento)** que coincida con el selector indicado.  
Si no encuentra coincidencias, devuelve `null`.

---

### 🔍 Ejemplo práctico

Supongamos el siguiente HTML:

```html
<article class="card">
  <div class="content">
    <p class="text">Texto de ejemplo</p>
  </div>
</article>
```

Y el siguiente código:

```js
const texto = document.querySelector(".text");

const contenedor = texto.closest(".card");
console.log(contenedor); // <article class="card">...</article>
```

En este caso, el método **recorre el árbol hacia arriba** desde `.text` hasta encontrar el primer ancestro que cumpla el selector `.card`.

---

### 🧩 Diferencia con `parentElement`

- `parentElement` devuelve **solo el padre inmediato** (sin condiciones).
    
- `closest()` busca **hacia arriba** todos los ancestros y devuelve **el primero que cumpla** con el selector indicado.
    

Por ejemplo:

```js
console.log(texto.parentElement);     // <div class="content">
console.log(texto.closest(".card"));  // <article class="card">
```

---

### ⚠️ Consideraciones importantes

- Si el propio elemento cumple la condición, `closest()` **lo devuelve a sí mismo**.
    
- Si no encuentra ningún elemento que cumpla el selector, devuelve **`null`**.
    
- La búsqueda **se detiene en el nodo raíz del documento**, por lo que nunca recorrerá más allá de `document`.
    

---

### 💡 Uso práctico común

Un uso típico de `closest()` es en la **delegación de eventos**, donde se necesita determinar desde qué elemento específico del DOM se disparó un evento, pero dentro de una estructura compleja.

Ejemplo:

```js
document.addEventListener("click", e => {
  const card = e.target.closest(".card");
  if (card) {
    console.log("Hiciste clic dentro de una tarjeta:", card);
  }
});
```

Aquí, sin importar si el clic ocurrió en el texto, en un botón o en una imagen dentro de `.card`,  
`closest()` nos permite detectar el **contenedor principal relevante**.

---

## 🧭 Conclusión general del módulo

El recorrido por los nodos del DOM —sus hijos, padres y hermanos— culmina con la comprensión de su estructura interna (`nodeType`) y con el método `closest()`, que brinda una forma más inteligente de navegar hacia los ancestros.

Ambos conceptos cierran el ciclo de **navegación de nodos**:  
uno desde la **identificación** (saber qué tipo de nodo tenemos),  
y el otro desde la **búsqueda contextual** (saber a qué elemento superior pertenece).

---
