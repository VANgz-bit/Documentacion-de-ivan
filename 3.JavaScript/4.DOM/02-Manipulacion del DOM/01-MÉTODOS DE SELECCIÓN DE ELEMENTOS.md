-# 📘 MANIPULACIÓN DEL DOM — MÉTODOS DE SELECCIÓN DE ELEMENTOS

---

## 🧩 1. Concepto general

El primer paso para manipular el DOM con JavaScript es **acceder a los elementos del documento**, es decir, obtener una **referencia directa** a los nodos del árbol DOM.

El objeto `document` representa la raíz del DOM (es decir, el nodo de tipo `Document`) y es el punto de partida para buscar cualquier otro elemento dentro de la página.  
A partir de él, el navegador nos ofrece diferentes métodos de selección, cada uno con sus **propias características**, **velocidad de búsqueda**, y **forma de devolver los resultados**.

Los métodos de selección pueden clasificarse según:

- Si devuelven **uno o varios elementos**.
    
- Si la colección devuelta es **viva o estática**.
    
- Si utilizan **identificadores estructurados (id, clase, etiqueta)** o **selectores CSS**.
    

Veamos cada uno en detalle.

---

## 🔹 2. `getElementById(id)`

### 🧠 Descripción

Devuelve una **referencia directa** al **único elemento** del documento cuyo atributo `id` coincide con el valor especificado.  
Si no se encuentra ningún elemento con ese `id`, devuelve `null`.

Este método es **uno de los más rápidos y eficientes**, ya que el navegador mantiene un **mapa interno** de los `id` para acceder a ellos directamente sin recorrer todo el árbol DOM.

### 📄 Sintaxis

```js
document.getElementById("idElemento")
```

### 🧩 Ejemplo práctico

```html
<p id="mensaje">Hola Mundo</p>
<script>
  const parrafo = document.getElementById("mensaje");
  console.log(parrafo.textContent); // "Hola Mundo"
</script>
```

### 📘 Características importantes

- **No usa el prefijo `#`** (como en CSS).
    
- Si el `id` se repite (lo cual es incorrecto en HTML), el método **solo devolverá el primero** que encuentre.
    
- Si se ejecuta antes de que el DOM esté cargado, devolverá `null`.
    
- Solo puede usarse sobre el objeto `document`, no sobre otros nodos.
    

### ⚙️ Caso especial

Si por error hay varios elementos con el mismo `id`:

```html
<p id="mensaje">Uno</p>
<p id="mensaje">Dos</p>

<script>
  console.log(document.getElementById("mensaje").textContent); // "Uno"
</script>
```

Solo devuelve el primero encontrado en el orden del documento.

---

## 🔹 3. `getElementsByClassName(nombreClase)`

### 🧠 Descripción

Devuelve una **colección viva (`HTMLCollection`)** de todos los elementos que poseen la clase indicada en su atributo `class`.  
“Viva” significa que si el DOM cambia (por ejemplo, se agrega o elimina un elemento con esa clase), la colección se actualiza automáticamente.

### 📄 Sintaxis

```js
document.getElementsByClassName("nombreClase")
```

### 🧩 Ejemplo práctico

```html
<div class="caja"></div>
<div class="caja"></div>

<script>
  const cajas = document.getElementsByClassName("caja");
  console.log(cajas.length); // 2
</script>
```

### 📘 Características

- Se puede acceder por **índice numérico**: `cajas[0]`, `cajas[1]`.
    
- Es sensible al **espacio en nombres de clases**:
    
    ```html
    <div class="caja grande"></div>
    ```
    
    Puede obtenerse con `getElementsByClassName("caja")` o con `getElementsByClassName("grande")`.
    
- Se puede invocar sobre cualquier nodo del DOM, no solo sobre `document`:
    
    ```js
    const seccion = document.getElementById("contenedor");
    const hijos = seccion.getElementsByClassName("item");
    ```
    

### ⚙️ Caso especial

Si agregamos un nuevo elemento con esa clase, **la colección cambia automáticamente**:

```js
const cajas = document.getElementsByClassName("caja");
console.log(cajas.length); // 2

const nuevaCaja = document.createElement("div");
nuevaCaja.classList.add("caja");
document.body.appendChild(nuevaCaja);

console.log(cajas.length); // 3 (actualizado)
```

---

## 🔹 4. `getElementsByTagName(nombreEtiqueta)`

### 🧠 Descripción

Devuelve una **colección viva (`HTMLCollection`)** de todos los elementos que tienen el nombre de etiqueta especificado (por ejemplo: `"div"`, `"p"`, `"li"`, etc.).

### 📄 Sintaxis

```js
document.getElementsByTagName("etiqueta")
```

### 🧩 Ejemplo práctico

```html
<p>Uno</p>
<p>Dos</p>

<script>
  const parrafos = document.getElementsByTagName("p");
  console.log(parrafos[1].textContent); // "Dos"
</script>
```

### 📘 Características

- Al igual que el método anterior, devuelve una **colección viva**.
    
- También puede invocarse sobre un elemento concreto, por ejemplo:
    
    ```js
    const seccion = document.querySelector("section");
    const parrafos = seccion.getElementsByTagName("p");
    ```
    
    En este caso, solo se buscan los `p` dentro de esa `section`.
    
- Es ideal cuando se necesita recorrer todos los elementos de un tipo.
    

---

## 🔹 5. `querySelector(selector)`

### 🧠 Descripción

Devuelve el **primer elemento** que coincida con el selector CSS proporcionado.  
Este método permite usar **cualquier selector CSS válido**, lo que lo convierte en el método más flexible para seleccionar elementos.

### 📄 Sintaxis

```js
document.querySelector("selectorCSS")
```

### 🧩 Ejemplo práctico

```html
<p class="texto">Hola</p>
<p class="texto">Chau</p>

<script>
  const primerTexto = document.querySelector(".texto");
  console.log(primerTexto.textContent); // "Hola"
</script>
```

### 📘 Características

- Acepta cualquier selector CSS:
    
    - `.clase`
        
    - `#id`
        
    - `div > p`
        
    - `input[type="text"]`
        
    - `section article:first-child`
        
- Devuelve **solo el primer elemento coincidente**.
    
- Es **más lento** que `getElementById()` o `getElementsByClassName()` si se usa en grandes documentos, pero mucho más **preciso**.
    
- Si no se encuentra nada, devuelve `null`.
    

---

## 🔹 6. `querySelectorAll(selector)`

### 🧠 Descripción

Devuelve una **NodeList estática** (no viva) con todos los elementos que coincidan con el selector CSS proporcionado.  
A diferencia de `getElementsByClassName()` o `getElementsByTagName()`, la colección **no se actualiza automáticamente** si el DOM cambia.

### 📄 Sintaxis

```js
document.querySelectorAll("selectorCSS")
```

### 🧩 Ejemplo práctico

```html
<p class="texto">Hola</p>
<p class="texto">Chau</p>

<script>
  const textos = document.querySelectorAll(".texto");
  textos.forEach(el => console.log(el.textContent));
  // "Hola"
  // "Chau"
</script>
```

### 📘 Características

- Acepta cualquier selector CSS, incluso combinaciones complejas.
    
- Permite usar métodos de array como `.forEach()` para recorrer los elementos.
    
- La lista devuelta **no se actualiza** aunque se agreguen o eliminen nodos posteriormente.
    
- Se puede convertir fácilmente a un array si se desea:
    
    ```js
    const elementos = Array.from(document.querySelectorAll("div"));
    ```
    

---

## 🧾 7. Diferencias entre `HTMLCollection` y `NodeList`

|Propiedad|`HTMLCollection`|`NodeList`|
|---|---|---|
|Tipo de colección|Viva (se actualiza)|Estática (no cambia)|
|Devuelto por|`getElementsByClassName`, `getElementsByTagName`|`querySelectorAll`|
|Se actualiza con cambios en el DOM|✅ Sí|❌ No|
|Acceso por índice|✅ Sí|✅ Sí|
|Uso de `forEach()`|❌ En algunos navegadores antiguos|✅ Sí|
|Compatible con `for...of`|✅ Sí|✅ Sí|

---

## 🔹 8. Buenas prácticas

1. **Usar `getElementById()`** siempre que sea posible:  
    Es el método más rápido y directo para elementos únicos.
    
2. **Evitar abusar de colecciones vivas** en loops grandes:  
    Pueden producir **re-renderizados innecesarios** si el DOM se modifica dentro del mismo ciclo.
    
3. **Guardar referencias** a los elementos que se usarán varias veces:  
    Evita búsquedas repetidas que impactan en el rendimiento.
    
    ```js
    const btn = document.getElementById("boton");
    btn.addEventListener("click", accion);
    ```
    
4. **`querySelector()` y `querySelectorAll()`** son más modernos y flexibles,  
    por lo tanto, son los **más usados actualmente**, especialmente en proyectos grandes.
    

---

## 🔹 9. Esquema visual del proceso

```plaintext
document (raíz del DOM)
│
├── getElementById("id") → Element (único)
│
├── getElementsByClassName("clase") → HTMLCollection (viva)
│
├── getElementsByTagName("etiqueta") → HTMLCollection (viva)
│
├── querySelector("selectorCSS") → Element (primer match)
│
└── querySelectorAll("selectorCSS") → NodeList (estática)
```

---

