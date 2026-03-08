# 📘 `Symbol` en JavaScript – Documentación Completa

---

## 🔹 1. Definición

En JavaScript, **`Symbol`** es un **tipo de dato primitivo único e inmutable**, introducido en **ES6 (ECMAScript 2015)**.  
Se utiliza principalmente para **crear identificadores únicos** que no colisionen con otros valores, incluso aunque tengan el mismo nombre.

Características clave:

- Cada **`Symbol` es único**. Aunque dos símbolos tengan la misma descripción, nunca serán iguales.
    
- Sirve como **clave de propiedades en objetos** → evitando conflictos con otras propiedades o métodos.
    
- Tiene usos internos en JavaScript: los llamados **Well-Known Symbols**, que permiten personalizar comportamientos del lenguaje.
    

Ejemplo básico:

```js
let id1 = Symbol("usuario");
let id2 = Symbol("usuario");

console.log(id1 === id2); // false → cada Symbol es único
```

---

## 🔹 2. Sintaxis

La creación de un símbolo se hace con el constructor `Symbol()`.

```js
let simbolo = Symbol([descripcion]);
```

- **`descripcion`** (opcional): cadena que describe el símbolo, solo para propósitos de depuración (no afecta a su identidad).
    

Ejemplo:

```js
let clave = Symbol("id");
console.log(clave); // Symbol(id)
```

---

## 🔹 3. Características

1. **Primitivo único** → siempre genera un valor distinto.
    
2. **Inmutable** → no se puede cambiar una vez creado.
    
3. **No se convierte automáticamente en string o número**.  
    (Hay que hacerlo explícitamente con `toString()`).
    
4. **Se usa como clave de propiedad oculta en objetos**.  
    No aparece en `for...in` ni en `Object.keys()`.
    
5. **Evita colisiones** en propiedades de objetos.
    
6. Existen **Well-Known Symbols** que permiten redefinir cómo funcionan estructuras internas del lenguaje.
    

---

## 🔹 4. Ejemplos

✅ **Ejemplo bueno – Identificadores únicos:**

```js
let clave1 = Symbol("id");
let clave2 = Symbol("id");

console.log(clave1 === clave2); // false
```

✅ **Ejemplo bueno – Usar Symbol como clave en objeto:**

```js
let usuario = {
  nombre: "Iván",
  [Symbol("id")]: 123
};

console.log(usuario); // { nombre: "Iván", Symbol(id): 123 }
```

❌ **Ejemplo malo – Intentar comparar símbolos por descripción:**

```js
let a = Symbol("test");
let b = Symbol("test");

console.log(a == b); // false ❌
```

❌ **Ejemplo malo – Conversión implícita a string:**

```js
let s = Symbol("hola");
console.log("Mensaje: " + s); // ❌ TypeError
```

✅ Forma correcta:

```js
console.log("Mensaje: " + s.toString()); // "Mensaje: Symbol(hola)"
```

---

## 🔹 5. Casos especiales o curiosos

- **Propiedades ocultas en objetos:**
    

```js
let claveSecreta = Symbol("clave");
let persona = {
  nombre: "María",
  [claveSecreta]: "12345"
};

console.log(Object.keys(persona)); // ["nombre"] → no muestra el Symbol
console.log(persona[claveSecreta]); // "12345"
```

- **Acceder a propiedades Symbol:**
    

```js
let simbolos = Object.getOwnPropertySymbols(persona);
console.log(simbolos); // [ Symbol(clave) ]
```

- **Global Symbol Registry (`Symbol.for`)**:  
    Permite reutilizar símbolos con el mismo identificador en toda la aplicación.
    

```js
let a = Symbol.for("usuario");
let b = Symbol.for("usuario");

console.log(a === b); // true → porque se usa el registro global
```

---

## 🔹 6. Well-Known Symbols

Son símbolos predefinidos por JavaScript que permiten modificar el comportamiento de operaciones internas.  
Algunos ejemplos:

- **`Symbol.iterator`** → permite que un objeto sea iterable (`for...of`).
    
- **`Symbol.toPrimitive`** → define cómo se convierte un objeto a primitivo.
    
- **`Symbol.toStringTag`** → personaliza la etiqueta de un objeto en `Object.prototype.toString`.
    

Ejemplo con `Symbol.iterator`:

```js
let miObjeto = {
  datos: [1, 2, 3],
  [Symbol.iterator]() {
    let i = 0;
    let datos = this.datos;
    return {
      next() {
        return i < datos.length
          ? { value: datos[i++], done: false }
          : { done: true };
      }
    };
  }
};

for (let valor of miObjeto) {
  console.log(valor); // 1, 2, 3
}
```

---

## 🔹 7. Buenas prácticas

- Usar `Symbol` cuando se necesiten **claves únicas en objetos**.
    
- No abusar de `Symbol.for`, ya que rompe la unicidad.
    
- Usar descripciones (`Symbol("desc")`) para depuración clara.
    
- Evitar convertir símbolos automáticamente a strings.
    
- Usar **Well-Known Symbols** solo cuando realmente necesites redefinir comportamientos avanzados.
    

---

## 🔹 8. Resumen

- `Symbol` es un **primitivo único e inmutable**.
    
- Se usa para crear **identificadores únicos**, en especial como **claves de propiedades ocultas**.
    
- No es convertible automáticamente a string.
    
- Tiene soporte de un **registro global (`Symbol.for`)**.
    
- Existen **Well-Known Symbols** para modificar comportamientos internos del lenguaje.
    

---
