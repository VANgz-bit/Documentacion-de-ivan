
# 📘 Operadores de corto circuito en JavaScript

---

## 1. Concepto general

En JavaScript, cuando hablamos de **corto circuito** nos referimos al comportamiento especial de algunos **operadores lógicos** (`||` y `&&`), que hacen que la evaluación de una expresión se detenga tan pronto como ya no sea necesario seguir evaluando.

Este fenómeno ocurre porque:

- El operador **OR (`||`)** está diseñado para devolver el **primer valor verdadero (truthy)** que encuentre.
    
- El operador **AND (`&&`)** está diseñado para devolver el **primer valor falso (falsy)** que encuentre.
    

El resultado **no necesariamente es un booleano** (`true` o `false`), sino que puede ser cualquier valor evaluado en la expresión.

👉 Este comportamiento fue aprovechado durante años por los desarrolladores para implementar soluciones prácticas, especialmente en épocas en que el lenguaje no ofrecía formas modernas de trabajar con **valores por defecto**, **encadenamiento seguro**, o **validación de parámetros**.

---

## 2. Operador OR (`||`)

### Definición

El operador lógico **OR (`||`)** evalúa de izquierda a derecha y devuelve el **primer valor que sea truthy**.  
Si ninguno de los valores es truthy, devuelve el **último valor**.

### Reglas

- Si el primer valor ya es **truthy**, no evalúa el resto (se corta la ejecución).
    
- Si todos los valores son **falsy**, devuelve el último.
    

### Ejemplos explicados

```js
console.log("Hola" || "Mundo"); 
// "Hola" → truthy, la evaluación se corta aquí.

console.log(0 || "Mundo");      
// 0 es falsy → pasa al siguiente → "Mundo" (truthy) → resultado "Mundo".

console.log(null || 0 || false); 
// null → falsy, 0 → falsy, false → falsy → resultado final: false.
```

---

## 3. Operador AND (`&&`)

### Definición

El operador lógico **AND (`&&`)** evalúa de izquierda a derecha y devuelve el **primer valor falsy**.  
Si todos los valores son truthy, devuelve el **último**.

### Reglas

- Si el primer valor es falsy, se detiene ahí (corte inmediato).
    
- Si todos son truthy, devuelve el último valor.
    

### Ejemplos explicados

```js
console.log("Hola" && "Mundo");  
// Ambos truthy → devuelve el último → "Mundo".

console.log(0 && "Mundo");       
// 0 es falsy → corta aquí → resultado: 0.

console.log("Hola" && null);     
// "Hola" es truthy → sigue, null es falsy → resultado: null.
```

---

## 4. Usos prácticos tradicionales (antes de ES6)

### 4.1. Valores por defecto

Antes de que existieran los **parámetros por defecto** en funciones, se usaba `||` para asignar valores por defecto:

```js
function saludar(nombre) {
  nombre = nombre || "Desconocido";
  console.log("Hola " + nombre);
}

saludar("Iván");   // Hola Iván
saludar();         // Hola Desconocido
```

Problema: cualquier valor falsy (`""`, `0`, `false`) sería reemplazado, incluso cuando a veces esos valores eran válidos.

---

### 4.2. Ejecución condicional con `&&`

El operador `&&` también se usaba (y todavía se usa) como una forma compacta de ejecutar algo solo si se cumple una condición:

```js
let logueado = true;
logueado && console.log("Bienvenido!"); 
// Imprime "Bienvenido!" porque logueado es true

let logueado2 = false;
logueado2 && console.log("No deberías ver esto");
// No se ejecuta porque logueado2 es false
```

---

### 4.3. Evitar errores en objetos nulos o indefinidos

Otro uso común era validar con `&&` antes de acceder a propiedades que podrían no existir:

```js
let usuario = null;
let nombre = usuario && usuario.nombre; 
console.log(nombre); // null (en vez de romper el programa con un error)
```

Esto evitaba que JavaScript intentara acceder a `usuario.nombre` cuando `usuario` era `null` o `undefined`.

---

## 5. Mejoras modernas de JavaScript

Con la evolución del lenguaje, se introdujeron nuevas formas de hacer lo mismo pero de forma más clara y precisa.

---

### 5.1. Parámetros por defecto (ES6)

Desde ES6 se pueden definir parámetros con un valor por defecto directamente en la firma de la función:

```js
function saludar(nombre = "Desconocido") {
  console.log("Hola " + nombre);
}

saludar("Iván"); // Hola Iván
saludar();       // Hola Desconocido
```

Esto reemplaza la técnica de `nombre = nombre || "Desconocido"`.

---

### 5.2. Operador Nullish Coalescing (`??`) – ES2020

El operador `??` se creó porque `||` considera muchos valores falsy (como `0` o `""`) y los descartaba, incluso cuando eran válidos.

- `||` ignora: `false`, `0`, `""`, `null`, `undefined`, `NaN`.
    
- `??` solo ignora: `null` y `undefined`.
    

Ejemplo:

```js
let cantidad = 0;

console.log(cantidad || 10); // 10 (descarta el 0 porque es falsy)
console.log(cantidad ?? 10); // 0 (respeta el valor válido 0)
```

👉 Esto hace que `??` sea mucho más seguro para valores por defecto.

---

### 5.3. Optional Chaining (`?.`) – ES2020

El **encadenamiento opcional** es una forma moderna de evitar errores al acceder a propiedades de objetos que pueden ser nulos o indefinidos.

Ejemplo sin `?.`:

```js
let usuario = null;
console.log(usuario.nombre); 
// ❌ Error: no se puede leer 'nombre' de null
```

Ejemplo con `?.`:

```js
let usuario = null;
console.log(usuario?.nombre); 
// ✅ undefined (no lanza error, corta la evaluación)
```

Incluso se puede usar en cadenas más largas:

```js
let sistema = { usuario: { perfil: { nombre: "Iván" } } };

console.log(sistema?.usuario?.perfil?.nombre); // "Iván"
console.log(sistema?.config?.tema);            // undefined
```

---

## 6. Casos prácticos y explicación

### Caso 1: Valor por defecto con `||`

```js
let usuario = "" || "Invitado";
console.log(usuario); // "Invitado" porque "" es falsy
```

👉 Inconveniente: si realmente quería que el usuario fuese `""`, lo pierdo.

---

### Caso 2: Valor por defecto con `??`

```js
let usuario = "" ?? "Invitado";
console.log(usuario); // "" porque solo null y undefined son ignorados
```

👉 Aquí se respeta el valor válido aunque sea una cadena vacía.

---

### Caso 3: Validar existencia antes de ejecutar

```js
let boton = true;
boton && console.log("El botón fue presionado");
// ✅ Solo ejecuta si boton es true
```

---

### Caso 4: Encadenamiento seguro

```js
let config = null;

let tema1 = config && config.tema; 
console.log(tema1); // null (corto circuito con &&)

let tema2 = config?.tema; 
console.log(tema2); // undefined (opcional chaining)
```

---

## 7. Resumen completo

- **Corto circuito** es la detención anticipada de la evaluación en operadores lógicos.
    
- **`||` (OR)** devuelve el primer **truthy** o el último si todos son falsy.
    
- **`&&` (AND)** devuelve el primer **falsy** o el último si todos son truthy.
    
- Usos tradicionales:
    
    - Valores por defecto (`nombre = nombre || "..."`).
        
    - Validación de objetos (`obj && obj.prop`).
        
    - Ejecución condicional (`condicion && accion`).
        
- Mejoras modernas:
    
    - **Parámetros por defecto** (ES6).
        
    - **Nullish coalescing (`??`)** para valores por defecto más seguros.
        
    - **Optional chaining (`?.`)** para acceso seguro a propiedades.
        

---
