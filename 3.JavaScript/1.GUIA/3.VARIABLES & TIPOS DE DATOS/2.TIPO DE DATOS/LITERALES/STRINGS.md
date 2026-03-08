# 📘 Cadenas Literales en JavaScript

## 🔹 Definición

Una **cadena literal** (string literal) es una secuencia de **cero o más caracteres** encerrados entre **comillas simples (`'`)**, **comillas dobles (`"`)** o **comillas invertidas (`` ` `` en ES2015, llamadas _backticks_)**.  
Se usan para representar **texto** en el código fuente de un programa.

En otras palabras, una cadena literal es la forma más directa de escribir un valor de tipo `string` en JavaScript.

---

## 🔹 Sintaxis básica

```js
'texto en comillas simples';
"texto en comillas dobles";
```

- Ambos delimitadores (`'` y `"`) son válidos.
    
- Se debe **abrir y cerrar con el mismo tipo de comillas**.
    
- Si se necesita incluir comillas dentro de la cadena, se pueden escapar con `\` o alternar el tipo de comillas.
    

Ejemplos:

```js
"John's cat"      // ✅ válido (uso de comillas dobles para incluir apóstrofe)
'El dijo: "Hola"' // ✅ válido (uso de comillas simples para incluir comillas dobles)
'No\'s vemos'     // ✅ usando barra invertida para escapar
```

---

## 🔹 Caracteres especiales (escape sequences)

Dentro de las cadenas se pueden usar **secuencias de escape** con `\` para representar caracteres especiales:

```js
"una linea \n otra linea" // salto de línea
"tab\tseparado"           // tabulación
"\\ruta\\archivo"         // barra invertida
"\"texto entre comillas\""// comillas dobles
```

---

## 🔹 Uso de propiedades y métodos de `String`

Aunque las **cadenas literales** son valores primitivos, JavaScript las convierte automáticamente en un **objeto `String` temporal** cuando invocamos métodos o accedemos a propiedades.

Ejemplo:

```js
console.log("Hola".length);      // 4  (propiedad .length)
console.log("Hola".toUpperCase()); // "HOLA"
```

Esto funciona porque el motor crea un objeto `String` detrás de escena, ejecuta la operación, y luego lo descarta.

---

## 🔹 Plantillas literales (Template literals, ES2015+)

A partir de ES2015, se introdujo una nueva forma de escribir cadenas con **backticks (`` ` ``)**.  
Estas permiten características adicionales:

### 1. Cadenas multilínea

```js
let texto = `Esto es una cadena
que ocupa más de una línea`;
console.log(texto);
```

### 2. Interpolación de variables

Se pueden insertar expresiones dentro de una cadena usando `${expresión}`:

```js
let nombre = "Iván";
let edad = 21;
console.log(`Hola, me llamo ${nombre} y tengo ${edad} años.`);
// "Hola, me llamo Iván y tengo 21 años."
```

### 3. Etiquetas en plantillas (Tagged templates)

Permiten procesar el contenido de la cadena antes de crearla.  
Ejemplo típico para evitar inyecciones o procesar datos:

```js
function safe(strings, ...values) {
  return strings.reduce((acc, str, i) => acc + str + (values[i] || ""), "");
}

let user = "<script>alert('xss')</script>";
console.log(safe`Usuario: ${user}`);
// Usuario: <script>alert('xss')</script>
```

---

## 🔹 Casos especiales

1. **Cadena vacía**:
    
    ```js
    let vacia = "";
    console.log(vacia.length); // 0
    ```
    
    Representa la ausencia de caracteres.
    
2. **Inmutabilidad**:  
    Las cadenas en JavaScript son **inmutables**, lo que significa que no se pueden modificar directamente.
    
    ```js
    let saludo = "Hola";
    saludo[0] = "M"; // ❌ no funciona
    console.log(saludo); // "Hola"
    ```
    
    Para cambiarla, hay que crear una nueva:
    
    ```js
    saludo = "M" + saludo.slice(1);
    console.log(saludo); // "Mola"
    ```
    
3. **Objeto String vs literal string**:
    
    ```js
    let literal = "Hola";             // cadena literal (primitivo)
    let objeto = new String("Hola"); // objeto String
    console.log(typeof literal); // "string"
    console.log(typeof objeto);  // "object"
    ```
    
    > ⚠️ Se recomienda usar **cadenas literales** salvo casos muy específicos.
    

---

## 🔹 Buenas prácticas

- Preferir **cadenas literales** (`'texto'`, `"texto"`) para la mayoría de los casos.
    
- Usar **template literals** (`` ` ``) cuando se necesiten variables interpoladas o cadenas multilínea.
    
- Evitar usar el constructor `new String()` porque genera confusiones entre primitivos y objetos.
    
- Escapar los caracteres especiales siempre que sea necesario para evitar errores de sintaxis.
    

---

## 📌 Resumen

- Las **cadenas literales** son la forma más común de representar texto en JavaScript.
    
- Se escriben entre `'`, `"`, o `` ` ``.
    
- JavaScript permite acceder a métodos de `String` incluso en literales.
    
- Desde ES2015, las **template literals** mejoran la legibilidad y permiten interpolación y multilíneas.
    
- Las cadenas son **inmutables**, lo que implica que cualquier modificación genera una nueva cadena.
    

---
