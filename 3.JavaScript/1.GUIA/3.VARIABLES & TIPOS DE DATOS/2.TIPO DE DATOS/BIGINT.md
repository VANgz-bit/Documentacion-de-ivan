# 📘 `BigInt` en JavaScript – Documentación Completa

---

## 🔹 1. Definición general de `BigInt`

**`BigInt`** es un tipo de dato primitivo en JavaScript que permite representar **enteros de cualquier tamaño**, incluso aquellos que **superan los límites seguros de los números (`Number`) de 64 bits**.

A diferencia de `Number`, que se basa en el estándar **IEEE 754 de doble precisión (64 bits, coma flotante)** y solo puede representar enteros con precisión hasta `±(2^53 - 1)`, `BigInt` no tiene este límite y mantiene la **precisión exacta** en cálculos con enteros grandes.

👉 `BigInt` fue introducido en **ES2020** y está disponible en todos los navegadores modernos.

---

## 🔹 2. Sintaxis de `BigInt`

Existen **dos formas** de declarar un `BigInt`:

### 2.1 Usando el sufijo `n` (forma literal)

```js
let numeroGrande = 123456789012345678901234567890n;
```

📌 El sufijo `n` al final del número convierte el literal en un `BigInt`.

---

### 2.2 Usando el constructor `BigInt()`

```js
let numeroGrande = BigInt("123456789012345678901234567890");
```

📌 Se puede pasar un número o una cadena que represente un número entero.  
⚠️ Si la cadena contiene decimales o caracteres inválidos → `SyntaxError`.

---

## 🔹 3. Características de `BigInt`

1. **Representa enteros arbitrariamente grandes** → no limitado a 64 bits.
    
2. **Mantiene precisión exacta** → ideal para cálculos financieros, criptografía o conteo de datos enormes.
    
3. **Solo admite enteros** → no puede representar fracciones ni decimales.
    
4. **No se puede mezclar con `Number` sin conversión** → hay que convertir explícitamente.
    
5. **División entera** → los decimales se truncan automáticamente.
    
6. **Compatibilidad parcial** → algunos métodos de `Math` no soportan `BigInt` (`Math.sqrt`, `Math.pow`, etc.).
    

---

## 🔹 4. Ejemplos

### 4.1 Ejemplo bueno

```js
let a = 9007199254740991n; // MAX_SAFE_INTEGER
let b = 2n;
console.log(a + b); // 9007199254740993n ✅
```

👉 Con `Number`, este cálculo se perdería por imprecisión.

---

### 4.2 Ejemplo malo (mezcla de tipos)

```js
let a = 10n;
let b = 5;
console.log(a + b); // ❌ TypeError
```

👉 Solución:

```js
console.log(a + BigInt(b)); // ✅ 15n
```

---

### 4.3 División entera

```js
console.log(5n / 2n); // 2n ✅ (se trunca el decimal)
console.log(5 / 2);   // 2.5 con Number
```

---

### 4.4 Uso con constructor

```js
let x = BigInt("12345678901234567890");
console.log(x); // 12345678901234567890n
```

---

## 🔹 5. Casos especiales o curiosos

- **No soporta decimales**
    

```js
10.5n // ❌ SyntaxError
```

- **No es intercambiable con `Number`**
    

```js
BigInt(10.5); // ❌ RangeError
BigInt(10);   // ✅ 10n
```

- **Conversión implícita peligrosa**
    

```js
console.log(Number(10n) + 5); // 15 ✅
console.log(Number(123456789012345678901234567890n)); 
// 1.2345678901234568e+29 ⚠️ pierde precisión
```

---

## 🔹 6. Buenas prácticas

1. Usar `BigInt` solo cuando realmente se necesiten **enteros enormes**.
    
2. Convertir explícitamente entre `Number` y `BigInt` para evitar errores de tipo.
    
3. No usar `BigInt` para cálculos con decimales → preferir librerías como **Decimal.js**.
    
4. Para valores muy grandes, comparar siempre con `BigInt`, no con `Number`.
    
5. Evitar mezclar `BigInt` en lógica matemática tradicional (`Math`) porque no todos los métodos lo soportan.
    

---

## 🔹 7. Resumen

- 🔹 `BigInt` es un **tipo de dato primitivo** que permite representar enteros de cualquier tamaño con precisión exacta.
    
- 🔹 Se declara con `n` al final del número o con `BigInt()`.
    
- 🔹 No admite decimales ni fracciones.
    
- 🔹 No se mezcla con `Number` directamente → requiere conversión explícita.
    
- 🔹 La división siempre devuelve un entero truncado.
    
- 🔹 Útil en cálculos financieros, criptográficos o de conteo de datos masivos.
    

---