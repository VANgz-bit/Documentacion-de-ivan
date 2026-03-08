---

# 🧭 Clases, `classList` y el objeto `DOMTokenList`

---
# 🧭 Clases, `classList` y el objeto `DOMTokenList`

---

## 📘 1. Introducción conceptual

El atributo `class` de un elemento HTML cumple un papel central en la estructura y el estilo de las páginas web.  
Permite asignar **una o más clases CSS** que definen el aspecto visual o la identificación de grupos de elementos con un propósito común.

En el DOM, este atributo se representa mediante dos propiedades principales:

- `element.className`
    
- `element.classList`
    

Ambas permiten leer y modificar las clases, pero lo hacen de forma diferente:

- `className` maneja el contenido del atributo como una **cadena de texto (string)**.
    
- `classList`, en cambio, devuelve un **objeto vivo** de tipo `DOMTokenList`, el cual gestiona cada clase como un **token independiente**, permitiendo manipularlas con métodos específicos y evitando errores comunes.
    

---

## 🧩 2. El atributo `class` dentro del DOM

En la estructura del árbol DOM, el atributo `class` forma parte del **nodo de tipo elemento**.  
Su contenido se almacena como una cadena única dentro del atributo `class`, pero cuando se accede mediante la propiedad `classList`, el motor del navegador **convierte automáticamente esa cadena en una colección estructurada** de tokens.

Diagrama:

```
Nodo <p class="azul grande centrado">
│
├── Atributo "class" → "azul grande centrado"
│
└── Propiedad classList → DOMTokenList ["azul", "grande", "centrado"]
```

Esta conversión es dinámica:  
si modificamos `classList`, el atributo `class` se actualiza;  
si cambiamos el atributo directamente, el `DOMTokenList` también se ajusta automáticamente.

---

## 🧠 3. `className` vs `classList`: diferencias estructurales

**`className`** es simplemente un alias directo del atributo HTML.  
Al asignarle un nuevo valor, reemplaza completamente todas las clases existentes.

```js
element.className = "rojo grande";
```

**`classList`**, en cambio, devuelve una **instancia viva de `DOMTokenList`**, un tipo de objeto especialmente diseñado para representar **listas de tokens únicos** (palabras separadas por espacios) dentro de los atributos HTML.

Esto significa que no se trata de una cadena, sino de una **colección iterable** de valores que puede modificarse sin reemplazar todo el contenido.

---

## 🔍 4. El objeto `DOMTokenList` en profundidad

### 📘 Definición formal

`DOMTokenList` es una interfaz que representa una **lista ordenada de cadenas únicas**, donde cada elemento se llama **token**.  
Cada token se corresponde con una palabra dentro del atributo que se esté representando (en este caso, el atributo `class`).

El DOM usa `DOMTokenList` no solo para `classList`, sino también en otros contextos como:

- el atributo `rel` en enlaces (`<link rel="stylesheet preload">`),
    
- o el atributo `sandbox` en iframes (`<iframe sandbox="allow-scripts allow-forms">`).
    

Esto demuestra que `DOMTokenList` es una **abstracción genérica** para representar cualquier atributo compuesto por una lista de identificadores separados por espacios.

---

### ⚙️ Comportamiento interno

Cada vez que se manipula un `DOMTokenList`, el navegador:

1. **Divide la cadena original del atributo** por espacios.
    
2. **Elimina duplicados**, ya que cada token debe ser único.
    
3. **Mantiene la lista sincronizada** con el atributo HTML original.
    

Esto hace que `DOMTokenList` funcione como una **vista en tiempo real** del atributo en cuestión.

Por ejemplo:

```html
<p id="demo" class="rojo grande centrado"></p>
```

```js
const el = document.getElementById("demo");

console.log(el.classList); // DOMTokenList ["rojo", "grande", "centrado"]

// Modificamos el DOMTokenList
el.classList.add("activo");

// Ahora el atributo HTML también cambia automáticamente:
console.log(el.getAttribute("class"));
// "rojo grande centrado activo"
```

---

### 💡 Relación con el árbol DOM

Cada nodo de tipo elemento posee internamente una estructura de atributos clave-valor.  
Cuando el motor del navegador detecta que un atributo representa una lista de tokens (como `class` o `rel`), **asocia automáticamente una instancia de `DOMTokenList`** para gestionar esa información.

Así, el `DOMTokenList`:

- pertenece al **nodo elemento**,
    
- actúa como una **capa intermedia** entre el atributo y el código JavaScript,
    
- y se actualiza automáticamente cuando cualquiera de los dos cambia.
    

---

## 🧩 5. Propiedades y métodos de `DOMTokenList`

A continuación se detalla cada miembro con su explicación técnica y ejemplos.

---

### 🔹 `length`

Devuelve la cantidad total de tokens presentes en la lista.

```js
console.log(el.classList.length); // 4
```

---

### 🔹 `value`

Devuelve todos los tokens en una cadena separada por espacios (similar a `className` pero sincronizada con la lista).

```js
console.log(el.classList.value); // "rojo grande centrado activo"
```

---

### 🔹 `item(index)`

Devuelve el token que se encuentra en la posición indicada (basado en índice, comenzando en 0).  
Si el índice no existe, devuelve `null`.

```js
console.log(el.classList.item(1)); // "grande"
```

---

### 🔹 `add(token1, token2, …)`

Agrega uno o más tokens al atributo si no existen.  
Ignora duplicados y actualiza automáticamente el DOM.

```js
el.classList.add("visible", "enmarcado");
```

---

### 🔹 `remove(token1, token2, …)`

Elimina uno o más tokens de la lista.  
Si alguno no existe, no produce error.

```js
el.classList.remove("activo", "centrado");
```

---

### 🔹 `contains(token)`

Devuelve `true` si el token especificado está presente, `false` en caso contrario.

```js
if (el.classList.contains("rojo")) {
  console.log("El elemento tiene la clase 'rojo'.");
}
```

---

### 🔹 `toggle(token, force)`

Alterna un token:

- lo agrega si no está,
    
- lo elimina si ya existe.  
    El parámetro opcional `force` permite forzar su estado.
    

```js
el.classList.toggle("oculto");        // agrega o quita
el.classList.toggle("activo", true);  // se asegura de agregar
el.classList.toggle("inactivo", false); // se asegura de eliminar
```

---

### 🔹 `replace(oldToken, newToken)`

Sustituye un token existente por otro.  
Si `oldToken` no existe, no hace nada.

```js
el.classList.replace("rojo", "verde");
```

---

### 🔹 Iteración

`DOMTokenList` es **iterable**, lo que significa que se puede recorrer con estructuras como `for...of`, `forEach()`, o convertir en un array.

```js
for (const clase of el.classList) {
  console.log(clase);
}
```

O usando el método `forEach()`:

```js
el.classList.forEach(c => console.log(c));
```

---

## 🧭 6. Ejemplo integrador completo

```html
<p id="parrafo" class="rojo grande centrado"></p>

<script>
  const p = document.getElementById("parrafo");

  console.log(p.classList); // DOMTokenList ["rojo", "grande", "centrado"]

  // Agregar y eliminar clases
  p.classList.add("visible", "bordeado");
  p.classList.remove("rojo");

  // Verificar existencia
  console.log(p.classList.contains("centrado")); // true

  // Alternar clases
  p.classList.toggle("oculto");
  p.classList.toggle("oculto"); // vuelve a quitarla

  // Reemplazar
  p.classList.replace("grande", "mediano");

  // Mostrar todas las clases actuales
  console.log([...p.classList]); // ["centrado", "visible", "bordeado", "mediano"]

  console.log(p.getAttribute("class")); // sincronizado
</script>
```

---

## 🧩 7. Diagrama de relación entre DOM, atributo y `DOMTokenList`

```
Nodo <p>
│
├── Atributo "class" = "centrado visible bordeado mediano"
│
├── Propiedad className = "centrado visible bordeado mediano"
│
└── Propiedad classList → DOMTokenList
       ├── Métodos: add(), remove(), contains(), toggle(), replace()
       ├── Propiedades: length, value
       └── Sincronización automática bidireccional
```

---

## 📘 8. Consideraciones y buenas prácticas

1. **`DOMTokenList` garantiza unicidad:** nunca habrá clases repetidas.
    
2. **Evitar concatenar cadenas en `className`**, ya que puede generar errores y duplicados.
    
3. **Usar `classList` en lugar de `className`** cuando se manipulan clases de forma dinámica.
    
4. Recordar que `DOMTokenList` refleja el estado actual del DOM: si se cambia el atributo `class` manualmente, `classList` se actualiza inmediatamente.
    
5. Cualquier modificación en `classList` provoca **un re-renderizado del elemento**, por lo que se debe evitar abusar de operaciones sucesivas en bucles grandes.
    

---

## 💬 Conclusión

- `classList` es una interfaz moderna y segura para manipular clases CSS.
    
- Su implementación se basa en la interfaz **`DOMTokenList`**, que actúa como una representación estructurada, sincronizada y iterable del atributo `class`.
    
- Gracias a `DOMTokenList`, el DOM puede mantener coherencia entre el HTML y el estado interno de los elementos, evitando duplicados y errores de sintaxis.
    
- Comprender cómo funciona `DOMTokenList` en el fondo permite dominar la manipulación de clases y entender mejor cómo el DOM gestiona atributos que contienen múltiples valores.
    

---

¿Querés que ahora sigamos con el siguiente punto del mapa —**Obtención y modificación de elementos**— con este mismo nivel de detalle y profundidad?