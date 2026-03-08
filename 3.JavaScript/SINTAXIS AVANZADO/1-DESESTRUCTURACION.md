# **Desestructuración en JavaScript**

## **1. ¿Qué es la desestructuración?**

La **desestructuración** es una **sintaxis que permite extraer valores de arrays o propiedades de objetos y asignarlos a variables de forma más concisa y legible**.

- Antes, para acceder a los valores de un objeto o array, se usaban múltiples líneas con notación de punto (`obj.propiedad`) o corchetes (`array[indice]`).
    
- Con la desestructuración, podemos **“desempaquetar” los valores directamente** en variables.
    

**Ventaja principal:**  
Reduce líneas de código, mejora la legibilidad y facilita el manejo de valores en funciones, parámetros o asignaciones.

---

## **2. Desestructuración de objetos**

### **2.1 Sintaxis básica**

```js
const persona = { nombre: "Iván", edad: 21, pais: "Argentina" };

// Desestructuración
const { nombre, edad, pais } = persona;

console.log(nombre); // "Iván"
console.log(edad);   // 21
console.log(pais);   // "Argentina"
```

**Explicación:**

- `{ nombre, edad, pais }` indica las propiedades que queremos extraer.
    
- Cada propiedad se asigna a una **variable con el mismo nombre**.
    
- Esto evita tener que escribir `persona.nombre`, `persona.edad`, etc.
    

---

### **2.2 Renombrar variables**

Podemos asignar un **nombre distinto** a la variable:

```js
const { nombre: n, edad: e } = persona;

console.log(n); // "Iván"
console.log(e); // 21
```

- `nombre: n` → extrae la propiedad `nombre` y la asigna a la variable `n`.
    
- Esto es útil para evitar conflictos de nombres o abreviar nombres largos.
    

---

### **2.3 Valores por defecto**

Si una propiedad **no existe**, podemos asignar un valor por defecto:

```js
const { nombre, ciudad = "Desconocida" } = persona;

console.log(ciudad); // "Desconocida"
```

- `ciudad` no existe en el objeto, así que toma el valor `"Desconocida"` automáticamente.
    

---

### **2.4 Desestructuración anidada**

Si un objeto contiene otros objetos, también podemos extraer valores internos:

```js
const usuario = {
  nombre: "Iván",
  direccion: {
    calle: "Calle Falsa 123",
    ciudad: "Buenos Aires"
  }
};

const { direccion: { calle, ciudad } } = usuario;

console.log(calle); // "Calle Falsa 123"
console.log(ciudad); // "Buenos Aires"
```

- Aquí desestructuramos un **objeto dentro de otro** directamente en variables.
    

---

## **3. Desestructuración de arrays**

### **3.1 Sintaxis básica**

```js
const numeros = [1, 2, 3];

const [a, b, c] = numeros;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```

- Cada posición del array se asigna a la variable correspondiente según el orden.
    
- `[a, b, c]` → `a = numeros[0]`, `b = numeros[1]`, etc.
    

---

### **3.2 Ignorar elementos**

Podemos omitir valores que no necesitamos:

```js
const [primero, , tercero] = numeros;

console.log(primero); // 1
console.log(tercero); // 3
```

- El **espacio vacío** indica que saltamos la posición que no queremos asignar (`2` en este caso).
    

---

### **3.3 Valores por defecto en arrays**

Si la posición no existe, podemos dar un valor predeterminado:

```js
const [x, y, z, w = 10] = numeros;

console.log(w); // 10
```

- `w` no existe en el array original, así que toma el valor `10`.
    

---

### **3.4 Desestructuración con el operador rest**

Podemos capturar **el resto de elementos** con `...`:

```js
const [primero, ...resto] = numeros;

console.log(primero); // 1
console.log(resto);   // [2, 3]
```

- `...resto` guarda los elementos restantes en un nuevo array.
    

---

## **4. Desestructuración en parámetros de funciones**

### **4.1 Objetos como parámetros**

```js
function saludar({ nombre, edad }) {
  console.log(`Hola ${nombre}, tienes ${edad} años`);
}

saludar(persona); // "Hola Iván, tienes 21 años"
```

- La función **extrae automáticamente** las propiedades del objeto recibido.
    

---

### **4.2 Arrays como parámetros**

```js
function suma([a, b]) {
  return a + b;
}

console.log(suma([5, 10])); // 15
```

- Se desestructura directamente el array pasado a la función, sin acceder por índice manualmente.
    

---

## **5. Buenas prácticas y consideraciones**

1. Usar desestructuración cuando queramos **acceder a varias propiedades o elementos** de manera clara.
    
2. Evitar nombres de variables que **confundan con otras existentes**; en objetos se puede renombrar.
    
3. Cuando el objeto o array **puede no tener ciertas propiedades o posiciones**, usar **valores por defecto**.
    
4. En objetos anidados o arrays complejos, la desestructuración mejora la legibilidad, pero **no abusar** de niveles muy profundos, puede dificultar el mantenimiento.
    

---
### importante: Hay mas tipos de destructuracion que mas adelante se definirán.