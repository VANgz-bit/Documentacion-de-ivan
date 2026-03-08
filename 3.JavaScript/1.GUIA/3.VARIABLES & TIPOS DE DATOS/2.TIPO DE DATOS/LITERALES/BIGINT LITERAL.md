# 🔹 Literales **BigInt** en JavaScript

## 📌 Definición

Un **literal BigInt** es una forma de escribir directamente en el código un número entero que puede ser **más grande que el máximo permitido por el tipo `Number`**.  
En JavaScript, el tipo `Number` usa la especificación **IEEE 754 de 64 bits en coma flotante**, lo que significa que solo puede representar enteros con precisión hasta **2⁵³ - 1 (≈ 9,007,199,254,740,991)**.  
Cuando necesitamos trabajar con valores enteros más grandes, entra en juego el tipo **BigInt**.

Para declarar un literal BigInt, simplemente se añade la letra **`n`** al final del número:

```js
1234567890123456789012345678901234567890n
```

Esto indica al motor de JavaScript que ese valor es un **BigInt** y no un `Number`.

---

## 📌 Sintaxis general

Un literal BigInt puede escribirse en diferentes **bases numéricas** (igual que los literales numéricos comunes):

- **Decimal (base 10):**
    
    ```js
    let decimal = 123456789n;
    ```
    
- **Binario (base 2, con prefijo `0b` o `0B`):**
    
    ```js
    let binario = 0b101010n; // equivale a 42
    ```
    
- **Octal (base 8, con prefijo `0o` o `0O`):**
    
    ```js
    let octal = 0o755n; // equivale a 493
    ```
    
- **Hexadecimal (base 16, con prefijo `0x` o `0X`):**
    
    ```js
    let hexadecimal = 0x1fffffffffffffn; // valor muy grande
    ```
    

> ⚠️ Importante: Siempre debe terminar en `n`. Si no, será interpretado como un `Number`.

---

## 📌 Características principales

1. **Precisión infinita en enteros:**  
    Puede representar números enteros de cualquier tamaño, positivo o negativo, sin pérdida de precisión.
    
    ```js
    let gigante = 999999999999999999999999999999999999n;
    console.log(giarante); 
    // se guarda exacto, sin redondeo
    ```
    
2. **Solo enteros:**  
    BigInt **no admite decimales**. Si intentás usar un punto decimal, obtendrás un error:
    
    ```js
    let invalido = 10.5n; // ❌ SyntaxError
    ```
    
3. **Operaciones matemáticas básicas:**  
    Se pueden usar operadores como `+`, `-`, `*`, `%`, `**` (exponenciación).
    
    ```js
    let a = 10n;
    let b = 3n;
    console.log(a + b); // 13n
    console.log(a * b); // 30n
    console.log(a ** b); // 1000n
    ```
    
4. **Restricción con `Number`:**  
    No se pueden mezclar `BigInt` y `Number` directamente en operaciones aritméticas.
    
    ```js
    let a = 5n;
    let b = 2;
    console.log(a + b); // ❌ TypeError
    ```
    
    Si necesitás mezclarlos, debés **convertir uno al otro**:
    
    ```js
    Number(a) + b; // convierte BigInt → Number
    a + BigInt(b); // convierte Number → BigInt
    ```
    

---

## 📌 Casos de uso

1. **Trabajar con grandes cantidades de datos científicos o financieros** donde los números exceden el rango de `Number`.
    
    ```js
    let universo = 123456789012345678901234567890n;
    ```
    
2. **Códigos hash o criptografía**, donde se manejan valores extremadamente grandes.
    
3. **Identificadores únicos** que superan el rango de enteros seguros (`Number.MAX_SAFE_INTEGER`).
    
    ```js
    let id = 9007199254740993n; // más allá del límite seguro
    ```
    

---

## 📌 Ejemplo completo

```js
// Ejemplo de operaciones con BigInt
let poblacionMundial = 7800000000n; 
let años = 100n;
let incremento = 10000000n; 

// Calcular población aproximada después de 100 años
let resultado = poblacionMundial + (incremento * años);

console.log(resultado); 
// 781000000000n
```

---

## ✅ Conclusión

Los **literales BigInt** son esenciales cuando trabajamos con enteros que superan la capacidad de un `Number`.  
Se escriben igual que los números comunes, pero llevan un **sufijo `n`**.  
Ofrecen **precisión ilimitada en enteros**, aunque no permiten decimales y requieren cierta precaución al mezclarse con `Number`.

---