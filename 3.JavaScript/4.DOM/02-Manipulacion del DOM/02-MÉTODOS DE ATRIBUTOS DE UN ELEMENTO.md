# 🧩 MÉTODOS DE ATRIBUTOS DE UN ELEMENTO 

## 1️⃣ Introducción: atributos en el DOM

En HTML, los **atributos** son información adicional que define características o comportamiento de un elemento. Cada elemento HTML es representado en el DOM como un **nodo de tipo Element**, y los atributos son accesibles y manipulables mediante métodos de JavaScript.

**Ejemplo en HTML:**

```html
<input type="text" id="nombre" class="campo" placeholder="Ingresa tu nombre" disabled>
```

- `type="text"` → define el tipo de input.
    
- `id="nombre"` → identificador único del elemento.
    
- `class="campo"` → clase para aplicar estilos.
    
- `placeholder="Ingresa tu nombre"` → texto guía que aparece dentro del input.
    
- `disabled` → atributo booleano, indica que el input está deshabilitado.
    

En el DOM, este input es un **nodo de tipo Element** y sus atributos pueden verse como **propiedades asociadas al nodo**, pero no siempre coinciden exactamente con las **propiedades del objeto DOM**.

---

## 2️⃣ Métodos principales de atributos

Los cuatro métodos fundamentales para manipular atributos son:

1. `getAttribute(nombre)` → Leer un atributo.
    
2. `setAttribute(nombre, valor)` → Crear o modificar un atributo.
    
3. `removeAttribute(nombre)` → Eliminar un atributo.
    
4. `hasAttribute(nombre)` → Verificar existencia de un atributo.
    

---

### 2.1 `getAttribute(nombre)`

**Función:** devuelve el valor actual del atributo indicado.

```js
const input = document.querySelector("input");
console.log(input.getAttribute("placeholder")); // "Ingresa tu nombre"
console.log(input.getAttribute("type"));        // "text"
console.log(input.getAttribute("disabled"));    // "" (en booleanos puede variar)
```

**Detalles importantes:**

- Siempre devuelve **un string o null** si el atributo no existe.
    
- Diferencia clave con la **propiedad del nodo**:
    

```js
console.log(input.disabled);       // true  (propiedad booleana)
console.log(input.getAttribute("disabled")); // "" o "disabled" (atributo)
```

- Los **atributos booleanos** (`disabled`, `checked`, `selected`) pueden devolver valores inesperados porque HTML solo requiere que existan para activarse.
    

**Diagrama conceptual:**

```
[Elemento input]
   ├─ atributo placeholder="Ingresa tu nombre"
   ├─ atributo type="text"
   └─ atributo disabled

getAttribute("placeholder") → devuelve "Ingresa tu nombre"
getAttribute("disabled") → devuelve "" o "disabled"
```

---

### 2.2 `setAttribute(nombre, valor)`

**Función:** crea un atributo si no existe o actualiza su valor si ya existe.

```js
input.setAttribute("value", "Iván");
input.setAttribute("data-role", "admin");
```

**Consideraciones:**

- `setAttribute` siempre trata **el valor como string**, incluso si la propiedad del DOM es booleana o numérica.
    
- Sirve para **atributos personalizados** `data-*`, esenciales para almacenar información extra sin modificar el HTML visible.
    
- Si el atributo ya existe, `setAttribute` lo sobrescribe.
    

**Ejemplo avanzado:**

```js
input.setAttribute("checked", "true"); // Activa el checkbox
console.log(input.checked); // true (propiedad reflejada)
```

---

### 2.3 `removeAttribute(nombre)`

**Función:** elimina el atributo indicado del elemento.

```js
input.removeAttribute("placeholder");
input.removeAttribute("disabled");
```

**Detalles:**

- Al eliminar un **atributo booleano**, la propiedad correspondiente se vuelve `false`.
    
- No lanza error si el atributo no existía.
    
- Útil para deshabilitar dinámicamente funcionalidades.
    

**Diagrama conceptual:**

```
[Elemento input]
   ├─ placeholder="Ingresa tu nombre"
   ├─ disabled
removeAttribute("disabled") → 
   └─ atributo disabled eliminado
   └─ propiedad input.disabled = false
```

---

### 2.4 `hasAttribute(nombre)`

**Función:** verifica si un atributo existe en el elemento.

```js
console.log(input.hasAttribute("placeholder")); // true
input.removeAttribute("placeholder");
console.log(input.hasAttribute("placeholder")); // false
```

**Notas:**

- Devuelve siempre **booleano** (`true`/`false`).
    
- Es muy útil antes de leer o modificar un atributo para evitar errores.
    

---

## 3️⃣ Diferencia entre **atributo** y **propiedad del nodo**

|Concepto|Qué representa|Ejemplo|
|---|---|---|
|**Atributo**|Lo que está declarado en HTML o mediante `setAttribute`|`<input disabled>` → atributo `disabled`|
|**Propiedad**|La representación del nodo en el objeto DOM|`input.disabled` → true/false|

**Ejemplo práctico:**

```html
<input id="test" type="checkbox" checked>
```

```js
const check = document.getElementById("test");

// Atributo
console.log(check.getAttribute("checked")); // "" (HTML solo requiere que exista)

// Propiedad
console.log(check.checked); // true (valor booleano real)
```

**Observación:** Aunque el atributo exista, la **propiedad refleja el estado actual real del elemento en la página**.

---

## 4️⃣ Ejemplo completo integrando los 4 métodos

```html
<input id="email" type="email" placeholder="Ingresa tu correo">
<button id="enviar" disabled>Enviar</button>
```

```js
const input = document.getElementById("email");
const boton = document.getElementById("enviar");

// Leer atributos
console.log(input.getAttribute("placeholder")); // "Ingresa tu correo"

// Modificar o crear atributos
input.setAttribute("value", "ivan@example.com");
input.setAttribute("data-role", "admin");

// Verificar existencia
console.log(boton.hasAttribute("disabled")); // true

// Eliminar atributos
boton.removeAttribute("disabled");
console.log(boton.hasAttribute("disabled")); // false
```

**Flujo en el DOM:**

```
[body]
 └─ [input#email]
      ├─ placeholder="Ingresa tu correo"
      ├─ value="ivan@example.com"
      └─ data-role="admin"
 └─ [button#enviar]
      └─ disabled eliminado → propiedad .disabled = false
```

---

✅ **Conclusión profunda**

Con estos métodos se logra **control total sobre los atributos de un elemento**, lo que permite:

- Modificar comportamiento dinámicamente (`disabled`, `checked`).
    
- Personalizar elementos con datos adicionales (`data-*`).
    
- Garantizar integridad antes de manipular propiedades mediante `hasAttribute`.
    
- Entender la relación entre **atributos declarados**, **propiedades del nodo** y el **estado real en el árbol DOM**.
    

---
