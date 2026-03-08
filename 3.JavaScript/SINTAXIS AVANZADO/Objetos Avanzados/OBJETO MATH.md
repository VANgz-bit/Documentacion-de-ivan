# 📘 Objeto `Math` en JavaScript

## 🔹 Definición General

El **objeto `Math`** en JavaScript es un objeto global que actúa como un **espacio de nombres matemático**: concentra un conjunto de **propiedades estáticas (constantes matemáticas)** y **métodos estáticos (funciones matemáticas comunes)** que nos permiten realizar operaciones numéricas de manera segura y eficiente.

Un aspecto fundamental es que **no es un constructor**; no podemos crear instancias con `new Math()`. Sus miembros son accesibles directamente:

```js
Math.PI;        // Propiedad
Math.round(4.5) // Método
```

En la práctica, `Math` es indispensable en áreas como:

- Procesamiento de datos numéricos.
    
- Programación gráfica y animaciones.
    
- Juegos y simulaciones físicas.
    
- Cálculos financieros, estadísticos y científicos.
    

---

# 🔹 Propiedades (Constantes Matemáticas)

El objeto `Math` incluye constantes que representan valores matemáticos universales.

### 1. **`Math.PI`**

Representa el número π, la relación entre la circunferencia y el diámetro de un círculo.

- Valor aproximado: `3.141592653589793`.
    
- Uso: geometría, trigonometría, cálculos de áreas y perímetros circulares.
    

📌 Ejemplo:

```js
console.log(Math.PI); // 3.141592653589793
```

---

### 2. **`Math.E`**

Representa el número de Euler, base de los logaritmos naturales.

- Valor aproximado: `2.718281828459045`.
    
- Uso: crecimiento exponencial, probabilidades y estadísticas.
    

📌 Ejemplo:

```js
console.log(Math.E); // 2.718281828459045
```

---

### 3. Otras constantes relevantes:

- **`Math.LN2`** → logaritmo natural de 2 (~0.693).
    
- **`Math.LN10`** → logaritmo natural de 10 (~2.302).
    
- **`Math.LOG2E`** → logaritmo en base 2 de e (~1.442).
    
- **`Math.LOG10E`** → logaritmo en base 10 de e (~0.434).
    
- **`Math.SQRT2`** → raíz cuadrada de 2 (~1.414).
    
- **`Math.SQRT1_2`** → raíz cuadrada de 1/2 (~0.707).
    

📌 Ejemplo:

```js
console.log(Math.SQRT2);   // 1.4142135623730951
console.log(Math.LOG10E);  // 0.4342944819032518
```

---

# 🔹 Métodos principales

## 1. **Métodos de redondeo y manipulación básica**

Estos métodos ajustan valores numéricos a formas más útiles en cálculos.

- **`Math.round(x)`**  
    Redondea `x` al entero más cercano.
    
    - `>= .5` se redondea hacia arriba.
        
    - `< .5` se redondea hacia abajo.
        
    
    ```js
    console.log(Math.round(4.4)); // 4
    console.log(Math.round(4.6)); // 5
    ```
    
- **`Math.floor(x)`**  
    Redondea siempre hacia abajo (hacia el entero menor).
    
    ```js
    console.log(Math.floor(4.9)); // 4
    console.log(Math.floor(-4.9)); // -5
    ```
    
- **`Math.ceil(x)`**  
    Redondea siempre hacia arriba (hacia el entero mayor).
    
    ```js
    console.log(Math.ceil(4.1)); // 5
    console.log(Math.ceil(-4.1)); // -4
    ```
    
- **`Math.trunc(x)`**  
    Elimina la parte decimal y se queda con la entera.
    
    ```js
    console.log(Math.trunc(4.9));  // 4
    console.log(Math.trunc(-4.9)); // -4
    ```
    
- **`Math.abs(x)`**  
    Devuelve el valor absoluto, eliminando el signo.
    
    ```js
    console.log(Math.abs(-7)); // 7
    ```
    

👉 **Aplicación práctica**: útil en cálculos financieros (ej. redondear precios), validación de coordenadas, límites en videojuegos.

---

## 2. **Potencias y raíces**

- **`Math.pow(base, exponente)`**  
    Devuelve la potencia de un número. Equivalente a `base ** exponente`.
    
    ```js
    console.log(Math.pow(2, 3)); // 8
    ```
    
- **`Math.sqrt(x)`**  
    Calcula la raíz cuadrada de `x`. Si `x < 0` devuelve `NaN`.
    
    ```js
    console.log(Math.sqrt(16)); // 4
    ```
    
- **`Math.cbrt(x)`**  
    Calcula la raíz cúbica.
    
    ```js
    console.log(Math.cbrt(27)); // 3
    ```
    
- **`Math.hypot(...valores)`**  
    Devuelve `√(a² + b² + …)` con varios argumentos. Esencial en geometría y vectores.
    
    ```js
    console.log(Math.hypot(3, 4)); // 5 (Teorema de Pitágoras)
    ```
    

👉 **Aplicación práctica**: física (distancias, velocidades), modelado 3D, cálculos estadísticos.

---

## 3. **Aleatoriedad**

- **`Math.random()`**  
    Devuelve un número pseudoaleatorio entre `0` (incluido) y `1` (excluido).
    

📌 Ejemplo:

```js
console.log(Math.random()); // Ej: 0.348573928492
```

👉 Para obtener un número entero en un rango:

```js
function aleatorio(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(aleatorio(1, 10)); // Ej: 7
```

👉 **Aplicación práctica**: juegos (dados, loterías), algoritmos de muestreo, testeo de datos.

---

## 4. **Máximos y mínimos**

- **`Math.max(...valores)`**  
    Devuelve el mayor de una lista de números.
    
    ```js
    console.log(Math.max(5, 10, 20, 3)); // 20
    ```
    
- **`Math.min(...valores)`**  
    Devuelve el menor.
    
    ```js
    console.log(Math.min(5, 10, 20, 3)); // 3
    ```
    

👉 **Aplicación práctica**: encontrar extremos en datasets, validar límites (ej. nivel de salud en un videojuego).

---

## 5. **Trigonometría**

Trabajan con radianes (no grados).

- **`Math.sin(x)`** → seno.
    
- **`Math.cos(x)`** → coseno.
    
- **`Math.tan(x)`** → tangente.
    
- **`Math.asin(x)`** → arcoseno (inverso del seno).
    
- **`Math.acos(x)`** → arcocoseno.
    
- **`Math.atan(x)`** → arcotangente.
    
- **`Math.atan2(y, x)`** → arcotangente considerando cuadrante (muy útil en gráficos).
    

📌 Ejemplo:

```js
console.log(Math.sin(Math.PI / 2)); // 1
console.log(Math.cos(0));           // 1
console.log(Math.tan(Math.PI / 4)); // 1
```

👉 **Aplicación práctica**: animaciones, movimiento de personajes, simulación de ondas, rotaciones en 2D/3D.

---

## 6. **Logaritmos y exponenciales**

- **`Math.exp(x)`**  
    Devuelve `e^x`.
    
    ```js
    console.log(Math.exp(1)); // 2.718
    ```
    
- **`Math.log(x)`**  
    Logaritmo natural (base e).
    
    ```js
    console.log(Math.log(Math.E)); // 1
    ```
    
- **`Math.log10(x)`**  
    Logaritmo en base 10.
    
    ```js
    console.log(Math.log10(100)); // 2
    ```
    
- **`Math.log2(x)`**  
    Logaritmo en base 2.
    
    ```js
    console.log(Math.log2(8)); // 3
    ```
    

👉 **Aplicación práctica**: modelado de crecimiento (financiero, biológico), escalas logarítmicas en gráficos, algoritmos de compresión.

---

# 🔹 Conclusión

El objeto `Math` es un **pilar matemático en JavaScript**, esencial tanto en programación cotidiana (redondeos, cálculos financieros) como en áreas más avanzadas (física, gráficos, simulaciones). Su fuerza radica en centralizar herramientas matemáticas sin necesidad de librerías externas.

---
