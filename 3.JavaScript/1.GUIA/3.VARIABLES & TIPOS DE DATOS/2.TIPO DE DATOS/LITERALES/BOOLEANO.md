# 🔹 Literales Booleanos en JavaScript

## 📖 Definición

Los **booleanos literales** son los valores primitivos `true` y `false` que representan las dos únicas posibilidades lógicas en JavaScript:

- `true` → verdadero
    
- `false` → falso
    

Estos valores son esenciales para controlar el flujo de un programa, ya que permiten tomar decisiones en condicionales, ciclos y expresiones lógicas.

---

## ⚡ Casos y usos principales

### 1. Condicionales

Se usan para decidir qué bloque de código ejecutar.

```js
let acceso = true;

if (acceso) {
  console.log("Acceso permitido");
} else {
  console.log("Acceso denegado");
}
```

👉 Aquí, el literal `true` hace que se ejecute la primera rama.

---

### 2. Comparaciones

Las operaciones de comparación siempre devuelven booleanos literales.

```js
console.log(5 > 3);     // true
console.log(10 === 2);  // false
```

👉 `>` y `===` generan valores booleanos automáticamente.

---

### 3. Estados o banderas (_flags_)

Se usan como indicadores para activar o desactivar opciones.

```js
let modoOscuro = false;
let notificacionesActivas = true;
```

👉 Muy útil para controlar configuraciones de usuario o estados internos.

---

### 4. Expresiones lógicas

Pueden combinarse con operadores lógicos (`&&`, `||`, `!`).

```js
let logueado = true;
let admin = false;

console.log(logueado && admin); // false
console.log(logueado || admin); // true
console.log(!admin);            // true
```

👉 Permite construir condiciones más complejas.

---

## ⚠️ Diferencia con el objeto `Boolean`

Aunque existen los objetos envoltorio `Boolean`, **no deben confundirse** con los literales.

- **Literal primitivo:** `true` o `false`.
    
- **Objeto Boolean:** creado con `new Boolean(valor)`.
    

Ejemplo:

```js
let primitivo = false;
let objeto = new Boolean(false);

console.log(primitivo);          // false
console.log(objeto);             // Boolean {false}
console.log(typeof primitivo);   // "boolean"
console.log(typeof objeto);      // "object"
```

👉 El objeto Boolean siempre es tratado como _truthy_ en evaluaciones, incluso si contiene `false`, lo que puede generar errores inesperados.

```js
if (new Boolean(false)) {
  console.log("Se ejecuta ❗"); // Sí se ejecuta, aunque parezca contradictorio
}
```

---

## ✅ Conclusión

- Los **booleanos literales** (`true`, `false`) son valores primitivos y básicos en cualquier programa.
    
- Son la base de la lógica condicional, bucles y evaluaciones en JavaScript.
    
- No deben confundirse con los objetos `Boolean`, que rara vez son necesarios y pueden causar confusión.
    

---