# 📘 Modificación de Elementos Obtenidos en el DOM

Cuando accedemos a un elemento del DOM, ese nodo no es una copia, sino una referencia directa al objeto que el navegador usa para representar el documento. Por lo tanto, toda modificación que hagamos sobre él se refleja inmediatamente en la página.  
A través de propiedades específicas, es posible cambiar su contenido, reemplazarlo o modificar su estructura interna. En esta etapa nos centraremos en tres propiedades fundamentales: `textContent`, `innerHTML` y `outerHTML`. Cada una de ellas opera sobre distintos niveles del nodo y produce efectos diferentes en el árbol del DOM.

---

## 🧩 `textContent`

La propiedad `textContent` permite acceder al contenido textual puro de un elemento, ignorando cualquier etiqueta HTML o estructura interna que contenga. Cuando se lee su valor, el navegador devuelve todo el texto presente dentro del elemento, incluyendo el de sus descendientes, pero sin interpretar formato alguno. Cuando se asigna un nuevo valor, todo el contenido interno se reemplaza por el texto indicado.

Por ejemplo:

```html
<p id="mensaje">Hola <strong>mundo</strong></p>

<script>
  const p = document.getElementById("mensaje");
  console.log(p.textContent); // Muestra: "Hola mundo"
  p.textContent = "Nuevo texto sin formato";
</script>
```

En este caso, el navegador toma el texto de todos los nodos de tipo texto que se encuentran dentro del párrafo y los combina en una sola cadena. Al escribir un nuevo valor, elimina los nodos hijos previos y crea un nuevo nodo de texto, reemplazando completamente el contenido anterior.  
Este comportamiento implica que cualquier etiqueta o estructura previa dentro del elemento desaparece. No se interpreta ninguna marca HTML, por lo que si se asigna algo como `<b>texto</b>`, se mostrará literalmente con los signos de menor y mayor.

Una característica importante es que `textContent` no altera el resto del árbol ni afecta a otros elementos: los cambios se limitan exclusivamente al nodo sobre el cual se aplica. Esto lo convierte en una herramienta segura para mostrar información generada dinámicamente, especialmente cuando proviene de fuentes externas o de usuario, ya que evita cualquier posibilidad de inyección de código HTML o JavaScript.

En resumen, `textContent` trabaja exclusivamente con texto plano, modificando o recuperando el contenido literal sin procesar etiquetas ni estructuras.

---

## 🧩 `innerHTML`

A diferencia de `textContent`, la propiedad `innerHTML` opera sobre el contenido **HTML estructurado** de un elemento. Al leer su valor, devuelve la representación en formato HTML de todos los nodos hijos. Al escribir un valor, el navegador interpreta la cadena como código HTML, crea los nodos correspondientes y reemplaza el contenido previo del elemento con el nuevo árbol generado.

Veamos un ejemplo:

```html
<div id="contenedor"></div>

<script>
  const div = document.getElementById("contenedor");
  div.innerHTML = "<p><strong>Texto con formato</strong> dentro del div.</p>";
</script>
```

En este caso, el valor asignado a `innerHTML` se analiza como HTML. El navegador construye internamente un nuevo conjunto de nodos: un elemento `<p>` que contiene otro `<strong>` y un texto. Luego, elimina cualquier nodo hijo anterior del `div` y los reemplaza por la nueva estructura.

Esta capacidad de interpretar HTML hace que `innerHTML` sea muy útil cuando se necesita insertar o modificar contenido que incluye etiquetas o estructuras completas, como bloques de texto con formato, listas o secciones enteras. Sin embargo, también implica un riesgo: si el contenido proviene de fuentes externas o no controladas, el navegador podría ejecutar código malicioso. Por eso, `innerHTML` solo debe usarse con contenido confiable o previamente filtrado.

Otra característica importante es que el navegador intenta corregir automáticamente los errores en el HTML que se le pasa. Si se omite una etiqueta de cierre o la estructura está incompleta, el motor de renderizado ajustará el código para mantener la coherencia del árbol. Aunque esto puede evitar errores visuales, también puede generar resultados inesperados si no se conoce este comportamiento.

En definitiva, `innerHTML` es una propiedad poderosa porque permite modificar secciones completas del documento con una sola operación, pero requiere precaución y comprensión de su efecto: al asignar un nuevo valor, todos los nodos hijos previos se destruyen y se crea un subárbol completamente nuevo dentro del elemento.

---

## 🧩 `outerHTML`

La propiedad `outerHTML` actúa en un nivel superior: no solo modifica el contenido interno del elemento, sino que también incluye al propio elemento en la operación. Al obtener su valor, devuelve el HTML completo que representa el nodo, incluyendo su etiqueta de apertura, sus atributos, el contenido interno y la etiqueta de cierre. Al establecer un nuevo valor, el navegador reemplaza todo el elemento —no solo su interior— por la estructura generada a partir del HTML asignado.

Ejemplo:

```html
<p id="texto">Hola Mundo</p>

<script>
  const p = document.getElementById("texto");
  console.log(p.outerHTML); // Muestra: "<p id='texto'>Hola Mundo</p>"
  p.outerHTML = "<h2>Nuevo encabezado</h2>";
</script>
```

Cuando se ejecuta la última línea, el elemento `<p>` desaparece completamente del DOM y es reemplazado por un nuevo elemento `<h2>`. El nodo original deja de existir dentro de la estructura del documento, y en su lugar se inserta el nuevo nodo creado a partir del HTML proporcionado.  
Esto significa que cualquier referencia en JavaScript que apunte al nodo anterior seguirá existiendo en memoria, pero ya no estará conectada al árbol DOM ni será visible en el documento. El navegador, internamente, destruye el nodo original y reconstruye otro en su misma posición dentro del árbol.

`outerHTML` resulta útil cuando se necesita sustituir un tipo de elemento por otro, o cuando se desea reemplazar completamente un bloque de contenido sin necesidad de eliminarlo manualmente. No obstante, su uso debe ser cuidadoso: dado que borra el nodo original, cualquier cambio previo o interacción asociada a él se pierde.

---
### 📘 Esquema comparativo: `textContent`, `innerHTML`, `outerHTML`

#### 🧩 Estado inicial del DOM

```
html
 └── body
      └── p
           └── "Hola mundo"
```

---

### 🔹 1. Modificación con `textContent`

**Acción:**

```js
p.textContent = "Nuevo texto plano";
```

**Resultado en el árbol DOM:**

```
html
 └── body
      └── p
           └── "Nuevo texto plano"
```

**Efecto:**

- Reemplaza el texto del nodo.
    
- No interpreta etiquetas HTML.
    
- Mantiene el mismo elemento `<p>`.
    
- El cambio se refleja inmediatamente en pantalla.
    

---

### 🔹 2. Modificación con `innerHTML`

**Acción:**

```js
div.innerHTML = "<p><strong>Texto con formato</strong></p>";
```

**Resultado en el árbol DOM:**

```
html
 └── body
      └── div
           └── p
                └── strong
                     └── "Texto con formato"
```

**Efecto:**

- Reemplaza todos los hijos del elemento `<div>`.
    
- Interpreta el contenido como HTML.
    
- Si hay etiquetas mal formadas, el navegador intenta corregirlas.
    
- Puede alterar completamente la estructura interna del DOM.
    

---

### 🔹 3. Modificación con `outerHTML`

**Acción:**

```js
p.outerHTML = "<h2>Nuevo encabezado</h2>";
```

**Resultado en el árbol DOM:**

```
html
 └── body
      └── h2
           └── "Nuevo encabezado"
```

**Efecto:**

- Reemplaza el elemento `<p>` completo por un nuevo nodo `<h2>`.
    
- El nodo original deja de existir en el DOM.
    
- Es útil para cambiar el tipo o estructura de un elemento.
    

---
## 🧠 Conclusión general

Las propiedades `textContent`, `innerHTML` y `outerHTML` constituyen los mecanismos fundamentales para modificar el contenido de los elementos del DOM. Aunque a simple vista parecen similares, cada una actúa sobre un nivel diferente del árbol:

- `textContent` opera únicamente sobre el texto plano del elemento.
    
- `innerHTML` gestiona la estructura interna y permite incluir etiquetas HTML.
    
- `outerHTML` reemplaza el nodo completo, incluyendo su propia etiqueta.
    

El dominio de estas propiedades permite comprender cómo el navegador interpreta, crea y destruye nodos dentro del documento, marcando la base de toda manipulación dinámica del DOM.

---

