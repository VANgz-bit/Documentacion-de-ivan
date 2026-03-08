# Sección 1: `Array`

# 1. Definición

Un **Array (arreglo)** es una **estructura de datos compuesta que permite almacenar múltiples valores dentro de una misma variable, organizados mediante índices numéricos consecutivos**.

Cada elemento dentro del arreglo ocupa una posición llamada **índice**, comenzando desde **0**, lo que significa que el primer elemento siempre se encuentra en la posición `0`.

En términos conceptuales:

> Un array es una colección ordenada de valores en la que cada elemento puede ser accedido mediante un índice numérico.

En TypeScript, los arrays permiten además **definir el tipo de datos que deben contener sus elementos**, lo cual introduce una restricción que no existe de manera formal en JavaScript.

---

# 2. Características fundamentales de los arrays

Los arrays presentan varias propiedades importantes:

1. **Son estructuras indexadas**
    
2. **Mantienen un orden de los elementos**
    
3. **Pueden contener múltiples valores**
    
4. **Permiten acceso directo mediante índice**
    
5. **Son objetos especiales en JavaScript**
    

Ejemplo conceptual:

```text
Índice:   0      1      2
Valor:  "rojo" "azul" "verde"
```

---

# 3. Declaración de arrays en TypeScript

TypeScript ofrece **dos formas principales de declarar arrays tipados**.

---

## Forma 1 — Notación con corchetes

Es la forma más utilizada.

### Ejemplo

```ts
let numeros: number[] = [1, 2, 3, 4];
```

Significado:

- `number[]` indica **un arreglo cuyos elementos deben ser números**.
    

---

### Ejemplo con strings

```ts
let nombres: string[] = ["Ana", "Pedro", "Iván"];
```

---

## Forma 2 — Usando el tipo genérico `Array<T>`

TypeScript también permite utilizar una sintaxis genérica.

```ts
let numeros: Array<number> = [1, 2, 3];
```

Esta forma es **funcionalmente equivalente** a:

```ts
let numeros: number[]
```

La primera es simplemente una forma **basada en generics**.

---

# 4. Inferencia de tipos en arrays

TypeScript puede **inferir automáticamente el tipo de un array** basándose en los valores iniciales.

### Ejemplo

```ts
let edades = [20, 30, 40];
```

TypeScript infiere:

```ts
number[]
```

---

### Ejemplo con strings

```ts
let colores = ["rojo", "azul", "verde"];
```

Tipo inferido:

```ts
string[]
```

---

# 5. Acceso a elementos del array

Los elementos se acceden mediante **índices numéricos**.

### Ejemplo

```ts
let frutas: string[] = ["manzana", "banana", "pera"];

console.log(frutas[0]);
```

Resultado:

```
manzana
```

---

# 6. Modificación de elementos

Los arrays permiten modificar valores utilizando el índice.

```ts
let numeros: number[] = [1, 2, 3];

numeros[1] = 10;
```

Resultado:

```text
[1, 10, 3]
```

---

# 7. Métodos comunes de arrays

Los arrays heredan múltiples métodos de JavaScript.

Ejemplos importantes:

|Método|Función|
|---|---|
|`push()`|agrega elementos al final|
|`pop()`|elimina el último elemento|
|`shift()`|elimina el primer elemento|
|`unshift()`|agrega al inicio|
|`map()`|transforma elementos|
|`filter()`|filtra elementos|
|`reduce()`|acumula valores|

---

### Ejemplo

```ts
let numeros: number[] = [1, 2, 3];

numeros.push(4);
```

Resultado:

```
[1,2,3,4]
```

---

# 8. Comparación entre arrays en JavaScript y TypeScript

### JavaScript

En JavaScript los arrays **no tienen restricción de tipo**.

```javascript
let datos = [1, "hola", true];
```

Esto es completamente válido.

---

### TypeScript

En TypeScript normalmente se define un tipo específico.

```ts
let datos: number[] = [1, 2, 3];
```

Si se intenta hacer:

```ts
datos.push("hola");
```

TypeScript generará un error.

---

# 9. Arrays con múltiples tipos

TypeScript permite definir arrays con **uniones de tipos**.

### Ejemplo

```ts
let datos: (number | string)[] = [1, "hola", 3];
```

Esto indica que el array puede contener:

- `number`
    
- `string`
    

---

# 10. Los arrays son objetos en JavaScript

Aunque conceptualmente se usan como listas, en JavaScript los arrays son **objetos especiales**.

Ejemplo:

```javascript
typeof []
```

Resultado:

```
"object"
```

Esto significa que los arrays heredan propiedades y métodos del prototipo `Array`.

---

# 11. Propiedad `length`

Los arrays poseen la propiedad `length`, que indica la cantidad de elementos.

### Ejemplo

```ts
let numeros: number[] = [1, 2, 3];

console.log(numeros.length);
```

Resultado:

```
3
```

---

# Conclusión

El tipo `Array` es una de las estructuras de datos más fundamentales tanto en JavaScript como en TypeScript. Representa una **colección ordenada de valores accesibles mediante índices numéricos**, y en TypeScript introduce una ventaja clave: **la posibilidad de restringir el tipo de los elementos que contiene**.

Esta característica mejora significativamente la seguridad del código, permitiendo detectar errores de tipo durante el desarrollo en lugar de en tiempo de ejecución.

---

