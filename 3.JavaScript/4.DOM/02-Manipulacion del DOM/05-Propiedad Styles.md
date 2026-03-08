# 🧭 Propiedad `style` en el DOM

La propiedad `style` es una de las interfaces más utilizadas en el **DOM (Document Object Model)** para manipular el aspecto visual de los elementos HTML desde JavaScript.  
Esta propiedad permite acceder y modificar directamente los **estilos en línea (inline styles)**, es decir, aquellos que se encuentran dentro del atributo `style` del propio elemento.

---

## 📘 1. Definición conceptual

En términos del **árbol DOM**, la propiedad `style` pertenece a los **nodos de tipo elemento** (por ejemplo, `<div>`, `<p>`, `<h1>`...).  
Cada nodo de este tipo contiene, entre otras cosas, un objeto interno llamado **`CSSStyleDeclaration`**, que representa todas las propiedades CSS definibles para ese elemento.

Por lo tanto, cuando usamos `element.style`, estamos accediendo a **una instancia de `CSSStyleDeclaration`** que contiene y gestiona los estilos **escritos directamente en el atributo `style`** del HTML.

Ejemplo inicial:

```html
<p id="texto" style="color: red; font-size: 20px;">Hola Mundo</p>
```

```js
const texto = document.getElementById("texto");
console.log(texto.style.color);     // "red"
console.log(texto.style.fontSize);  // "20px"
```

---

## 🧩 2. Naturaleza del objeto `style`

El objeto `style` **no es una cadena de texto**, sino un **objeto vivo** con una colección de propiedades que representan las reglas CSS aplicables al elemento.

A diferencia de la sintaxis CSS tradicional (que usa guiones `-`), JavaScript emplea **camelCase** para los nombres de las propiedades.

|Sintaxis en CSS|Sintaxis en JavaScript (`element.style`)|
|---|---|
|`background-color`|`backgroundColor`|
|`font-size`|`fontSize`|
|`text-align`|`textAlign`|

Ejemplo:

```js
texto.style.backgroundColor = "lightblue";
texto.style.textAlign = "center";
```

El cambio se refleja inmediatamente en el documento, porque el DOM re-renderiza el elemento afectado.

---

## 🧠 3. Diferencia entre `element.style` y los estilos aplicados desde CSS

Cuando trabajamos con estilos, debemos distinguir **de dónde provienen los valores**.  
El navegador puede aplicar estilos desde múltiples fuentes, pero el objeto `style` **solo representa los que están directamente escritos en el atributo `style` del elemento**.

### a) Estilos _inline_ (atributo `style`)

Estos se declaran directamente en el HTML:

```html
<p id="text" style="color: red;">Texto</p>
```

```js
const text = document.getElementById("text");
console.log(text.style.color); // "red"
```

El valor `"red"` está almacenado en el atributo `style`, por lo tanto es accesible y modificable con `element.style`.

---

### b) Estilos provenientes de CSS (internos o externos)

Cuando los estilos provienen de una hoja de estilo (`<style>` o `.css`), **no aparecen en `element.style`**, aunque sí se apliquen visualmente.

```html
<style>
  p {
    color: blue;
    font-size: 18px;
  }
</style>

<p id="text">Hola mundo</p>

<script>
  const text = document.getElementById("text");
  console.log(text.style.color); // "" → vacío
</script>
```

Esto ocurre porque `element.style` **no refleja los estilos computados**, sino únicamente los inline.

---

## 🧾 4. Obteniendo los estilos reales con `getComputedStyle()`

Para acceder a los valores **efectivamente aplicados** (incluyendo los heredados, los definidos en CSS y los valores por defecto del navegador), se utiliza el método `getComputedStyle(element)`.

Este método devuelve un objeto `CSSStyleDeclaration` que contiene **todos los estilos calculados** por el motor del navegador.

```html
<style>
  p {
    color: blue;
    font-size: 18px;
  }
</style>

<p id="text" style="margin-top: 10px;">Hola mundo</p>

<script>
  const text = document.getElementById("text");
  const estilos = getComputedStyle(text);

  console.log(estilos.color);      // "rgb(0, 0, 255)" (azul del CSS)
  console.log(estilos.fontSize);   // "18px" (CSS externo)
  console.log(estilos.marginTop);  // "10px" (inline)
</script>
```

**Importante:**

- `getComputedStyle()` es **de solo lectura**, no se puede modificar el estilo desde ahí.
    
- `element.style`, en cambio, **sí puede modificar estilos** pero solo los inline.
    

---

## ⚙️ 5. Comparación técnica

|Método|Qué devuelve|Fuente de los valores|Permite modificar|
|---|---|---|---|
|`element.style`|Estilos inline (atributo `style`)|HTML directo|✅ Sí|
|`getComputedStyle(element)`|Todos los estilos aplicados (inline, CSS, herencias, por defecto)|Motor de renderizado|❌ No|

---

## 💡 6. Ejemplo integrador completo

```html
<style>
  p {
    color: blue;
    font-size: 18px;
  }
</style>

<p id="text" style="margin-top: 10px;">Texto de ejemplo</p>

<script>
  const text = document.getElementById("text");

  // --- Usando element.style ---
  console.log(text.style.color); // "" → no está inline
  console.log(text.style.marginTop); // "10px" → sí está inline

  // --- Usando getComputedStyle() ---
  const estilos = getComputedStyle(text);
  console.log(estilos.color); // "rgb(0, 0, 255)" → azul del CSS
  console.log(estilos.fontSize); // "18px"
  console.log(estilos.marginTop); // "10px"

  // --- Modificando un estilo inline ---
  text.style.color = "green";
  console.log(text.style.color); // "green"
</script>
```

---

## 🧭 7. Esquema conceptual

```
Elemento HTML
│
├── Atributo "style" → Representado por element.style
│      │
│      └── Contiene estilos inline (CSSStyleDeclaration)
│
├── Hoja de estilo interna o externa
│      │
│      └── Gestionada por el motor de renderizado del navegador
│
└── Método getComputedStyle(element)
       └── Devuelve todos los estilos calculados finales
```

---

## 📘 8. Conclusión

- `element.style` permite leer y modificar **únicamente** los estilos inline.
    
- Para consultar **cómo se ve realmente** un elemento tras aplicar todas las reglas CSS, se usa `getComputedStyle()`.
    
- Ambas herramientas son complementarias: `element.style` modifica, `getComputedStyle()` inspecciona.
    
- Comprender esta diferencia es fundamental para trabajar correctamente con el **modelo visual del DOM** y depurar estilos de manera precisa.
    

---

¿