# 🧩 ATRIBUTOS DE LOS ELEMENTOS `<input>`

## 1️⃣ Introducción

Los elementos `<input>` son uno de los **pilares de la interacción en HTML**, ya que permiten **ingresar, seleccionar o manipular datos** dentro de formularios.

A diferencia de otros elementos, `<input>` posee un conjunto de **atributos propios y específicos**, además de los **atributos globales** que también puede tener (como `id`, `class`, `title`, `data-*`, etc.).

Estos atributos determinan **el tipo de dato que se espera**, **el comportamiento del campo**, y **las restricciones o validaciones** que aplican sobre el usuario.

En el DOM, cada atributo de un input tiene su **propiedad equivalente en el objeto del nodo**, lo que nos permite **leer, modificar y validar** dinámicamente los valores desde JavaScript.

---

## 2️⃣ Naturaleza de los atributos en `<input>`

El elemento `<input>` es **autocontenible** (no tiene etiqueta de cierre) y su comportamiento depende directamente del atributo `type`.  
Este atributo define **qué tipo de campo se crea**, y por tanto **qué otros atributos son relevantes o válidos**.

Por ejemplo:

```html
<input type="text" value="Iván">
<input type="checkbox" checked>
<input type="number" min="1" max="10" step="1">
```

Cada uno responde a distintos atributos y propiedades internas.

---

## 3️⃣ Atributos más importantes y su desarrollo completo

Veamos los principales, agrupándolos **por función real dentro del DOM**, y explicando cómo se manipulan desde JavaScript.

---

### 🔹 Atributo `type`

Define el **tipo de campo de entrada**.  
Su valor puede ser uno de muchos tipos predefinidos: `"text"`, `"password"`, `"email"`, `"number"`, `"checkbox"`, `"radio"`, `"file"`, `"color"`, `"date"`, `"range"`, entre otros.

Ejemplo:

```html
<input type="email">
```

Desde JavaScript:

```js
const input = document.querySelector("input");
console.log(input.type); // "email"

input.type = "text"; // Cambiamos tipo dinámicamente
```

**Consideraciones:**

- Cambiar el tipo puede **alterar el comportamiento y validación** del input.
    
- Algunos tipos como `"file"` o `"color"` tienen sus propias interfaces nativas del navegador.
    
- El tipo `"hidden"` lo excluye de la vista del usuario, pero sigue enviando su valor al formulario.
    

---

### 🔹 Atributo `value`

Representa **el valor actual del campo**, ya sea texto, número, o estado (según el tipo).  
Es **uno de los atributos más usados**, ya que es el que normalmente se envía al servidor o se procesa por JavaScript.

Ejemplo:

```html
<input type="text" value="Hola">
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.getAttribute("value")); // "Hola" → valor inicial del HTML
console.log(input.value); // "Hola" → valor actual

input.value = "Nuevo texto"; // Modificamos dinámicamente
```

**Diferencia entre atributo y propiedad:**

- `getAttribute("value")` devuelve el valor **original del HTML**.
    
- `input.value` devuelve el valor **actual modificado por el usuario o el script**.
    

Esto es una distinción clave al trabajar con formularios dinámicos.

---

### 🔹 Atributo `name`

Define **el nombre del campo** que se enviará al servidor al enviar el formulario.  
No afecta visualmente al input, pero es esencial para la **asociación con el backend**.

Ejemplo:

```html
<input type="text" name="usuario">
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.name); // "usuario"
input.name = "nombre_usuario";
```

- Si no se define `name`, el valor del input no se incluirá en los datos enviados por el formulario.
    
- `name` también es usado para **agrupar inputs tipo radio** (mismo `name` = mismo grupo).
    

---

### 🔹 Atributo `placeholder`

Muestra un **texto guía** dentro del campo cuando está vacío.  
No se envía como valor ni se considera parte del contenido.

Ejemplo:

```html
<input type="text" placeholder="Escriba su nombre">
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.placeholder); // "Escriba su nombre"
input.placeholder = "Nuevo texto de ayuda";
```

**Importante:**

- No reemplaza una etiqueta `<label>`; su función es orientativa.
    
- Se elimina automáticamente al escribir texto dentro del campo.
    

---

### 🔹 Atributos `checked` y `selected`

Afectan a **inputs booleanos** o seleccionables.

#### `checked`

Se aplica a `checkbox` y `radio`.  
Indica si el elemento está marcado.

```html
<input type="checkbox" checked>
```

JavaScript:

```js
const check = document.querySelector("input");
console.log(check.checked); // true
check.checked = false; // desmarcar
```

- `checked` es un atributo **booleano**: su mera presencia lo activa.
    
- La propiedad `.checked` refleja el **estado actual**, no solo el inicial.
    

#### `selected`

Se aplica a `<option>` dentro de `<select>`, no a `<input>`, pero sigue la misma lógica: si está presente, el valor se selecciona.

---

### 🔹 Atributo `disabled`

Desactiva el campo, impidiendo su edición o envío.  
El navegador lo renderiza visualmente atenuado y bloquea la interacción.

```html
<input type="text" value="No editable" disabled>
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.disabled); // true
input.disabled = false; // lo habilitamos
```

- Como `checked`, es un **atributo booleano**.
    
- Si está presente, el input no puede recibir foco ni eventos.
    
- Los inputs deshabilitados **no se envían** al servidor al enviar el formulario.
    

---

### 🔹 Atributos `readonly`, `required`, `autofocus`

Son booleanos también, pero con efectos distintos:

#### `readonly`

Permite ver el contenido pero no modificarlo.  
A diferencia de `disabled`, el campo **sí se envía** al servidor.

```html
<input type="text" value="Solo lectura" readonly>
```

#### `required`

Indica que el campo debe completarse antes de enviar el formulario.

```html
<input type="email" required>
```

#### `autofocus`

Hace que el campo reciba foco automáticamente al cargar la página.

```html
<input type="text" autofocus>
```

En JavaScript:

```js
const input = document.querySelector("input");
input.required = true;
input.readOnly = true;
```

---

### 🔹 Atributos de rango numérico (`min`, `max`, `step`)

Controlan los **límites y pasos** válidos en campos de tipo numérico (`number`, `range`, `date`, `time`, etc.).

Ejemplo:

```html
<input type="number" min="1" max="10" step="2" value="4">
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.min, input.max, input.step); // "1" "10" "2"

input.value = 9; // válido
input.value = 11; // inválido (puede rechazarse según navegador)
```

Estos atributos **no solo sirven visualmente**, también activan **validación automática** del navegador.

---

### 🔹 Atributo `pattern`

Define una **expresión regular (RegExp)** que el valor debe cumplir.  
Solo se aplica a tipos de texto, correo o contraseña.

```html
<input type="text" pattern="[A-Za-z]{3,10}" title="Debe tener entre 3 y 10 letras.">
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.pattern); // "[A-Za-z]{3,10}"
```

- Si el valor no coincide con el patrón, el formulario no se envía.
    
- `title` puede usarse para mostrar el mensaje de error personalizado.
    

---

### 🔹 Atributo `multiple`

Permite seleccionar o ingresar **más de un valor**, según el tipo.  
Se usa con `file` (para múltiples archivos) o `email` (para varios correos).

```html
<input type="file" multiple>
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.multiple); // true
```

---

### 🔹 Atributos de sugerencia y autocompletado

- **`list`** → enlaza el input con un `<datalist>` de sugerencias.
    
- **`autocomplete`** → activa o desactiva la función de autocompletado del navegador.
    

Ejemplo:

```html
<input type="text" list="nombres" autocomplete="on">
<datalist id="nombres">
  <option value="Iván">
  <option value="Lucas">
  <option value="Emmanuel">
</datalist>
```

JavaScript:

```js
const input = document.querySelector("input");
console.log(input.autocomplete); // "on"
```

---

## 4️⃣ Diagrama conceptual de los atributos de `<input>`

```
[<input> Elemento del DOM]
│
├── Tipo de entrada: type
│     ├─ text, number, email, checkbox, etc.
│
├── Valor y nombre
│     ├─ value
│     └─ name
│
├── Estado
│     ├─ checked / disabled / readonly / required / autofocus
│
├── Rango y validación
│     ├─ min / max / step / pattern
│
├── Apariencia y guía
│     ├─ placeholder / list / autocomplete
│
└── Multiplicidad
      └─ multiple
```

---

## 5️⃣ Conclusión general

Los atributos de `<input>` definen cómo se comporta, valida e interpreta un campo de entrada.  
Comprenderlos en detalle es crucial, porque:

- Muchos atributos se reflejan como **propiedades del nodo en el DOM** (por ejemplo, `input.value`, `input.checked`).
    
- Otros controlan **validación automática y experiencia del usuario** (`required`, `pattern`, `min`, `max`).
    
- Algunos son puramente **visuales o de guía** (`placeholder`, `list`, `autocomplete`).
    

Saber manipularlos desde JavaScript mediante los **métodos de atributos** o las **propiedades directas** nos permite **control total sobre los formularios y la interacción del usuario**.

---
