# 📘 `undefined` en JavaScript – Documentación Completa

---

## 🔹 1. Definición

En JavaScript, **`undefined`** es un valor primitivo especial que indica que **algo no tiene valor asignado** o que **no está definido**.  
Se da en dos escenarios principales:

1. **Asignación implícita por el motor de JavaScript** → cuando declaramos una variable pero no le damos un valor inicial.
    
2. **Asignación explícita por el programador** → cuando queremos indicar manualmente que algo no está definido.
    

⚠️ Diferencia clave con `null`:

- `null` → ausencia **intencional** de valor.
    
- `undefined` → ausencia de valor por **defecto** o no inicialización.
    

Ejemplo básico:

```js
let usuario;
console.log(usuario); // undefined
```

Aquí, `usuario` fue declarada pero nunca se le asignó valor.

---

## 🔹 2. Sintaxis

Se puede asignar de forma explícita, aunque no es común:

```js
let variable = undefined;
```

Generalmente, aparece de forma **implícita**:

```js
let variable;
console.log(variable); // undefined
```

---

## 🔹 3. Características

1. Es un **valor primitivo** único.
    
2. Es el **valor por defecto** de variables no inicializadas.
    
3. Es el **valor por defecto** de parámetros no pasados a funciones.
    
4. Es el valor que devuelve una función **sin `return` explícito**.
    
5. Es un valor **falsy** (en contextos booleanos se evalúa como `false`).
    
6. Su tipo en `typeof` es `"undefined"`.
    

---

## 🔹 4. Ejemplos

✅ **Ejemplo bueno – Variable no inicializada:**

```js
let edad;
console.log(edad); // undefined
```

✅ **Ejemplo bueno – Parámetro no pasado:**

```js
function saludar(nombre) {
  console.log("Hola " + nombre);
}
saludar(); // "Hola undefined"
```

✅ **Ejemplo bueno – Función sin retorno:**

```js
function sumar(a, b) {
  let resultado = a + b;
}
console.log(sumar(2, 3)); // undefined
```

❌ **Ejemplo malo – Usar undefined manualmente para marcar vacío:**

```js
let carrito = undefined; // ❌ Mejor usar null
```

---

## 🔹 5. Casos especiales o curiosos

- **Comparaciones con `null`:**
    

```js
console.log(undefined == null);  // true (comparación laxa)
console.log(undefined === null); // false (comparación estricta)
```

- **Propiedades inexistentes en objetos:**
    

```js
let persona = {};
console.log(persona.nombre); // undefined
```

- **Acceso a índices inexistentes en arrays:**
    

```js
let numeros = [10, 20];
console.log(numeros[5]); // undefined
```

---

## 🔹 6. Buenas prácticas

- **No usar `undefined` como valor asignado manualmente** → para indicar vacío, usar `null`.
    
- **Siempre usar comparaciones estrictas (`===`)** para evitar confusión con `null`.
    
- **Inicializar variables** para evitar valores `undefined` inesperados.
    
- En funciones, usar **valores por defecto en parámetros**:
    

```js
function saludar(nombre = "invitado") {
  console.log("Hola " + nombre);
}
saludar(); // "Hola invitado"
```

---

## 🔹 7. Resumen

- `undefined` representa la **ausencia de valor por defecto**.
    
- Es asignado automáticamente a variables, parámetros o funciones sin valor.
    
- Es un **primitivo único** y su tipo es `"undefined"`.
    
- Es un valor **falsy**.
    
- No debe usarse de forma manual para marcar vacío → en su lugar usar `null`.
    
- Diferente de `null`:
    
    - `null` = vacío intencional.
        
    - `undefined` = no definido o no inicializado.
        

---