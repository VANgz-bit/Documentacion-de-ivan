# 🔹 Literales numéricos en JavaScript

Un **literal numérico** es la **forma directa de escribir valores numéricos en el código**.  
En JavaScript, estos literales se usan en cálculos, condiciones, índices de arrays, bucles, configuraciones de color, operaciones de bits, etc.

👉 Todos los literales numéricos pertenecen al tipo **`Number`**, excepto los de tipo **`BigInt`**.  
👉 Los `Number` usan **doble precisión de 64 bits (IEEE 754)**, lo que les da gran rango, pero también limitaciones de precisión.

---

## 📌 Tipos de literales numéricos

### 1. **Decimales (base 10)**

Son los más comunes, escritos con dígitos del 0 al 9.  
Pueden ser enteros o de **coma flotante (decimales con o sin exponente)**.

Ejemplos de **enteros decimales**:

```js
let edad = 21;
let temperatura = -5;
```

Ejemplos de **coma flotante**:

```js
let pi = 3.1415926;   // parte entera y fracción
let x = .5;           // equivalente a 0.5
let y = -3.1E+12;     // notación científica (1 × 10^12)
let z = .1e-23;       // notación científica con exponente negativo
```

📍 **Sintaxis de coma flotante** según MDN:

```
[(+|-)][dígitos].[dígitos][(E|e)[(+|-)]dígitos]
```

- `[(+|-)]` → signo opcional
    
- `[dígitos]` → parte entera y fraccionaria
    
- `(E|e)` → notación exponencial (científica)
    

---

### 2. **Hexadecimal (base 16)**

Prefijo `0x` o `0X`.  
Dígitos: `0–9` y letras `a–f` o `A–F`.

```js
let hex = 0x1A;   // 26 en decimal
let color = 0xff; // 255 en decimal
```

---

### 3. **Octal (base 8)**

Prefijo `0o` o `0O`.  
Dígitos válidos: `0–7`.

```js
let octal = 0o10;   // 8 en decimal
let permiso = 0o777; // 511 en decimal
```

---

### 4. **Binario (base 2)**

Prefijo `0b` o `0B`.  
Dígitos válidos: `0` y `1`.

```js
let bin = 0b1010; // 10 en decimal
let flag = 0b1111; // 15 en decimal
```

---

### 5. **BigInt como literal numérico**

Se agrega una **`n` al final del número**.  
Sirve para trabajar con enteros fuera del rango seguro de `Number` (±2^53 − 1).

```js
let grande = 123456789123456789123456789n;
```

⚠️ No se puede mezclar directamente con `Number`:

```js
10n + 5;   // ❌ Error
10n + 5n;  // ✅ Correcto
```

---

## 📌 Casos de uso

- **Decimal entero / flotante** → operaciones matemáticas generales.
    
- **Hexadecimal** → representación de colores (`0xff0000`), valores de memoria.
    
- **Octal** → permisos en sistemas Unix/Linux (`0o755`).
    
- **Binario** → operaciones a nivel de bits, flags, encripción.
    
- **BigInt** → cálculos con números enormes (criptografía, bases de datos).
    

---

## ⚠️ Advertencias importantes

1. Los literales `Number` tienen límite de precisión:
    
    - Enteros seguros → `-(2^53 - 1)` a `+(2^53 - 1)`.
        
    - Si necesitás más → usar `BigInt`.
        
2. La representación binaria provoca **errores de precisión** en decimales:
    
    ```js
    console.log(0.1 + 0.2); // 0.30000000000000004
    ```
    
3. Aunque `3.0` y `3` son escritos distinto, **son el mismo valor `Number`**.
    

---

## ✅ Conclusión

- Los **literales numéricos** son la forma de expresar números en JS.
    
- Se dividen en **decimales (enteros y de coma flotante), hexadecimales, octales, binarios y BigInt**.
    
- El subgrupo **coma flotante** es clave porque permite escribir números en **notación decimal y científica**.
    
- Recordá siempre las **limitaciones de precisión de `Number`** y recurrí a `BigInt` para enteros grandes.
    

---
