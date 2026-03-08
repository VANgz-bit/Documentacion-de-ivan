# **JSON — Datos estructurados en la web**

## 📌 ¿Qué es JSON?

JSON (JavaScript Object Notation) es un **formato de texto ligero y estructurado** para representar datos de forma que puedan ser fácilmente interpretados por diferentes sistemas y lenguajes de programación. A diferencia de la sintaxis de JavaScript, JSON **tiene reglas estrictas** que lo hacen un formato universal para el intercambio de datos. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))

- **Formato basado en texto**: legible por humanos y sencillo de generar o analizar por máquinas. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))
    
- **Independiente de lenguaje**: aunque origen en JavaScript, lo soportan cientos de lenguajes. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))
    
- **Estructura de datos clara**: representa objetos, arreglos, números, strings, booleanos y `null`. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))
    

### Ejemplo de JSON válido

```json
{
  "nombre": "María",
  "edad": 30,
  "activo": true,
  "intereses": ["programación", "tecnología"]
}
```

📌 **JSON no admite** funciones, métodos, comentarios ni valores como `undefined`. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))

---

# **Usos principales de JSON**

JSON es fundamental en el desarrollo web moderno porque permite:

1. **Intercambio de datos entre cliente y servidor**
    
    - APIs REST o GraphQL envían y reciben JSON.
        
    - Los navegadores interpretan JSON para actualizar interfaces. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
        
2. **Almacenar datos estructurados**
    
    - Archivos `.json` de configuración.
        
    - Web storage (LocalStorage, SessionStorage). ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
        
3. **Persistencia y caching ligero**
    
    - Guardar estado o preferencias en el navegador. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
        

JSON es más organizado que formatos como CSV, ya que puede **representar estructuras complejas y jerárquicas** como objetos dentro de arreglos o arreglos dentro de objetos. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Glossary/JSON?utm_source=chatgpt.com "JSON - Glosario de MDN Web Docs | MDN"))

---

# **Sintaxis de JSON (reglas importantes)**

JSON consta de dos tipos de estructuras básicas:

1. **Objetos**: pares clave–valor entre llaves `{}`
    
    ```json
    { "clave": "valor", "edad": 25 }
    ```
    
2. **Arreglos**: lista ordenada de valores entre corchetes `[]`
    
    ```json
    ["uno", "dos", "tres"]
    ```
    

**Reglas clave:**

- Las **claves deben ir entre comillas dobles**. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON?utm_source=chatgpt.com "JSON - JavaScript | MDN"))
    
- No se permiten **comas finales** después del último elemento. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON?utm_source=chatgpt.com "JSON - JavaScript | MDN"))
    
- Todos los valores deben ser tipos permitidos (string, number, boolean, null, objeto o arreglo). ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON?utm_source=chatgpt.com "JSON - JavaScript | MDN"))
    

---

# **Serialización y deserialización**

Estos términos describen **cómo transformamos datos entre estructuras internas en el programa y el formato JSON de texto**.

## 🧠 Serialización

### Definición formal

La **serialización** es el proceso de **convertir estructuras de datos (como objetos o arreglos en JavaScript) en una cadena de texto JSON** para poder enviarlos o almacenarlos.

Este proceso prepara los datos para:

- Transmitirlos por la red (p. ej., en una petición HTTP POST). ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    
- Guardarlos en almacenamiento persistente (LocalStorage, bases de datos simples). ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    

---

## 🧠 Deserialización

### Definición formal

La **deserialización** es el proceso inverso:

> Convertir una **cadena de texto JSON** en una estructura de datos usable (objetos o arreglos) dentro del lenguaje. ([Devdoc](https://www.devdoc.net/web/developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON.html?utm_source=chatgpt.com "Working with JSON data - Learn web development | MDN"))

Es esencial cuando se reciben datos de una API o servidor, para poder trabajar con ellos como objetos en lugar de texto sin formato. ([Devdoc](https://www.devdoc.net/web/developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON.html?utm_source=chatgpt.com "Working with JSON data - Learn web development | MDN"))

---

# **Métodos de JavaScript para trabajar con JSON**

JavaScript proporciona un objeto global estático llamado `JSON` que contiene los métodos para serializar y deserializar. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON?utm_source=chatgpt.com "JSON - JavaScript | MDN"))

---

## 📌 `JSON.stringify()`

### ¿Qué hace?

`JSON.stringify()` **serializa un valor de JavaScript**, es decir:

- Toma **objetos, arreglos o valores primitivos**.
    
- Los convierte en una **cadena de texto con formato JSON**. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    

### Sintaxis

```js
JSON.stringify(valor[, replacer[, space]])
```

- `valor`: el objeto o dato a convertir. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    
- `replacer`: (opcional) función o arreglo para controlar qué se incluye. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    
- `space`: (opcional) espacio o número que define indentación para legibilidad. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    

### Ejemplo sencillo

```js
const obj = { nombre: "Iván", edad: 21 };
const texto = JSON.stringify(obj);
console.log(texto);
// '{"nombre":"Iván","edad":21}'
```

📌 Importante:

- Valores como funciones, `undefined` o símbolos son omitidos o convertidos a `null` en arrays. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    
- El resultado siempre es una **cadena**. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify?utm_source=chatgpt.com "JSON.stringify() - JavaScript | MDN"))
    

### ¿Para qué sirve?

- Preparar datos para enviar al servidor en una petición HTTP con `fetch()` o `axios`. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    
- Almacenar un objeto en LocalStorage. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    

---

## 📌 `JSON.parse()`

### ¿Qué hace?

`JSON.parse()` **deserializa**, es decir:

- Toma una **cadena de texto JSON** válida.
    
- La convierte en el objeto o arreglo correspondiente en JavaScript. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON./parse?utm_source=chatgpt.com "JSON.parse() - JavaScript | MDN"))
    

### Sintaxis

```js
JSON.parse(textoJSON[, reviver])
```

- `textoJSON`: la cadena con formato JSON. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON./parse?utm_source=chatgpt.com "JSON.parse() - JavaScript | MDN"))
    
- `reviver`: (opcional) función para transformar valores durante el proceso. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON./parse?utm_source=chatgpt.com "JSON.parse() - JavaScript | MDN"))
    

### Ejemplo sencillo

```js
const texto = '{"nombre":"María","edad":30}';
const obj = JSON.parse(texto);
console.log(obj.edad); // 30
```

📌 Si el texto no es un JSON válido, `JSON.parse()` arroja un error `SyntaxError`. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/JSON./parse?utm_source=chatgpt.com "JSON.parse() - JavaScript | MDN"))

### ¿Para qué sirve?

- Convertir la respuesta JSON de una API en un objeto utilizable. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    
- Leer datos almacenados como texto JSON y trabajar con ellos. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    

---

# **Relación con HTTP y APIs**

Cuando usamos `fetch()` o Axios para hacer peticiones HTTP:

1. El servidor envía una respuesta en formato JSON (texto).
    
2. El cliente recibe esa cadena.
    
3. Para trabajar con ella como objeto, usamos `JSON.parse()` o métodos como `res.json()` que internamente hacen parse automático. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    

Para enviar datos:

1. Creamos un objeto en JavaScript.
    
2. Lo convertimos en texto JSON con `JSON.stringify()`.
    
3. Lo enviamos en el cuerpo de la petición HTTP. ([developer.mozilla.org](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON?utm_source=chatgpt.com "Trabajando con JSON - Aprende desarrollo web | MDN"))
    

---
