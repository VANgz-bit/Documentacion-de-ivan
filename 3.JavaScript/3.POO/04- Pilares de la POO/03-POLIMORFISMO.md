# 📘 Polimorfismo en JavaScript

---

## 🔹 Introducción al concepto

El **polimorfismo** es uno de los **cuatro pilares fundamentales de la Programación Orientada a Objetos (POO)** junto con la **herencia**, el **encapsulamiento** y la **abstracción**.

La palabra proviene del griego:

- **Poly** → muchos
    
- **Morphé** → forma
    

En programación, **polimorfismo significa “muchas formas”**, es decir, la capacidad de un mismo método o acción de comportarse de manera diferente según el objeto que lo ejecute.

Esto le da al software **flexibilidad y escalabilidad**, porque se pueden diseñar métodos con un mismo nombre que adapten su comportamiento a distintos contextos.

---

## 🔹 ¿Qué significa en la práctica?

En términos simples:

- Varias clases pueden compartir un mismo **método con igual nombre**, pero cada clase lo implementa de forma distinta.
    
- Desde el punto de vista del código, se invoca siempre al mismo método, pero el **resultado varía según el objeto que lo ejecute**.
    

Ejemplo simple:

```javascript
class Animal {
  hablar() {
    console.log("El animal hace un sonido.");
  }
}

class Perro extends Animal {
  hablar() {
    console.log("El perro ladra: ¡Guau!");
  }
}

class Gato extends Animal {
  hablar() {
    console.log("El gato maúlla: ¡Miau!");
  }
}

let perro = new Perro();
let gato = new Gato();

perro.hablar(); // "El perro ladra: ¡Guau!"
gato.hablar();  // "El gato maúlla: ¡Miau!"
```

🔎 Aquí:

- El método se llama igual: `hablar()`.
    
- Pero el **comportamiento cambia** en `Perro` y `Gato`.
    
- A esto se lo conoce como **polimorfismo por sobrescritura**.
    

---

## 🔹 Tipos de polimorfismo en JavaScript

Aunque JavaScript no es fuertemente tipado como Java o C#, **sí maneja diferentes formas de polimorfismo**.

### 1. Polimorfismo por sobrescritura (Overriding)

Ocurre cuando una **clase hija redefine un método** que hereda de la clase padre.

Ejemplo:

```javascript
class Vehiculo {
  mover() {
    console.log("El vehículo se mueve.");
  }
}

class Auto extends Vehiculo {
  mover() {
    console.log("El auto avanza por la carretera.");
  }
}

class Avion extends Vehiculo {
  mover() {
    console.log("El avión vuela por el cielo.");
  }
}

new Auto().mover();  // "El auto avanza por la carretera."
new Avion().mover(); // "El avión vuela por el cielo."
```

🔎 El mismo método (`mover`) produce **acciones distintas** según el objeto.

---
## 🔹 Polimorfismo por Sobrecarga (Overloading)

### 📖 Definición

En lenguajes como **Java, C++ o C#**, la sobrecarga (_method overloading_) significa que **una misma función puede definirse varias veces con la misma firma (nombre), pero con distintos parámetros (cantidad o tipos)**.

👉 Ejemplo en Java:

```java
class Calculadora {
    int sumar(int a, int b) {
        return a + b;
    }

    double sumar(double a, double b) {
        return a + b;
    }

    int sumar(int a, int b, int c) {
        return a + b + c;
    }
}
```

Aquí `sumar` está sobrecargado: **mismo nombre, distinta lista de parámetros**.

---

### 🚨 En JavaScript no existe el _overloading_ real

JavaScript **no soporta sobrecarga de métodos de forma nativa**, porque una función puede recibir cualquier número de parámetros sin importar cómo se defina.  
Si defines dos funciones con el mismo nombre, **la última reemplaza a la anterior**.

```js
function sumar(a, b) {
  return a + b;
}

function sumar(a, b, c) {
  return a + b + c;
}

console.log(sumar(2, 3));    // NaN (porque 'c' es undefined en la segunda versión)
console.log(sumar(2, 3, 4)); // 9
```

👉 Observa que **la primera definición se perdió**: solo queda la última versión.

---

### ✅ ¿Cómo simulamos _overloading_ en JavaScript?

Podemos usar varias técnicas para emular la sobrecarga:

#### 1. Uso de argumentos opcionales

```js
function sumar(a, b, c) {
  if (c !== undefined) {
    return a + b + c;
  }
  return a + b;
}

console.log(sumar(2, 3));    // 5
console.log(sumar(2, 3, 4)); // 9
```

#### 2. Uso de `arguments` (objeto interno)

```js
function sumar() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sumar(2, 3));       // 5
console.log(sumar(2, 3, 4));    // 9
console.log(sumar(1, 2, 3, 4)); // 10
```

#### 3. Uso del operador **REST**

```js
function sumar(...nums) {
  return nums.reduce((acc, n) => acc + n, 0);
}

console.log(sumar(2, 3));         // 5
console.log(sumar(2, 3, 4));      // 9
console.log(sumar(1, 2, 3, 4, 5)); // 15
```

👉 Con esto, aunque no exista sobrecarga estricta como en Java o C++, **logramos un comportamiento polimórfico** porque la función `sumar` **se adapta a la cantidad de parámetros recibidos**.

---

## 🔹 Polimorfismo por Duck Typing

### 📖 Definición

El término _duck typing_ viene de la frase en inglés:  
_"If it walks like a duck and quacks like a duck, then it is a duck."_  
(“Si camina como un pato y hace cuac como un pato, entonces es un pato”).

En programación, esto significa que **no importa el tipo explícito de un objeto**, sino que **importa si tiene las propiedades o métodos esperados para ser usado**.

👉 En otras palabras: _“lo que importa no es lo que el objeto es, sino lo que puede hacer”_.

---

### 🚀 Ejemplo en JavaScript

Supongamos que tenemos varias clases diferentes, pero todas tienen un método `volar`.

```js
class Pato {
  volar() {
    console.log("El pato bate sus alas y vuela");
  }
}

class Avion {
  volar() {
    console.log("El avión enciende sus motores y despega");
  }
}

class Superheroe {
  volar() {
    console.log("El superhéroe se eleva hacia el cielo");
  }
}

function hacerVolar(objeto) {
  objeto.volar();
}

let pato = new Pato();
let avion = new Avion();
let superman = new Superheroe();

hacerVolar(pato);      // "El pato bate sus alas y vuela"
hacerVolar(avion);     // "El avión enciende sus motores y despega"
hacerVolar(superman);  // "El superhéroe se eleva hacia el cielo"
```

👉 Observa que:

- `hacerVolar` no necesita saber si el objeto es un **Pato, Avión o Superhéroe**.
    
- Solo necesita que tenga el **método `volar()`**.
    
- Eso es _duck typing_: **comportamiento sobre tipo**.
    

---

### ⚖ Diferencia clave

- En lenguajes **fuertemente tipados** (Java, C++), debemos declarar tipos explícitamente (interfaces, herencia formal).
    
- En JavaScript, al ser **dinámico**, se adopta el _duck typing_: si el objeto cumple con la interfaz esperada (aunque no la declare formalmente), funciona.
    

---

## 📊 Comparación Overloading vs Duck Typing

|Aspecto|Overloading|Duck Typing|
|---|---|---|
|**Definición**|Una misma función con **múltiples versiones** según los parámetros.|Uso de objetos que **no importa su tipo**, sino los métodos/propiedades que tengan.|
|**Soporte en JS**|No existe formalmente, pero se **simula** con `arguments`, parámetros opcionales o `rest`.|Natural en JS, porque es dinámico y flexible.|
|**Ejemplo típico**|`sumar(2,3)` y `sumar(2,3,4)` se comportan distinto.|`hacerVolar()` funciona tanto con un `Pato`, un `Avión` o un `Superhéroe`.|
|**En qué se enfoca**|En los **parámetros**.|En los **métodos/propiedades** del objeto.|

---

## 🔑 Conclusión

- **Overloading en JS** no existe de manera nativa, pero se puede **simular** aprovechando que las funciones aceptan parámetros variables.
    
- **Duck typing** es una de las características más poderosas de JavaScript: no importa la clase o el tipo, mientras el objeto cumpla con la “forma” que esperamos.
    
- Ambos son **formas de polimorfismo**, pero aplicados desde distintos ángulos:
    
    - Uno en la **definición de funciones** (overloading).
        
    - Otro en el **uso de objetos** (duck typing).

---

## 🔹 Importancia del polimorfismo

El polimorfismo permite:

1. **Reutilización de código** → un mismo método puede aplicarse a múltiples tipos de objetos.
    
2. **Flexibilidad y escalabilidad** → es más fácil agregar nuevas clases sin modificar el código existente.
    
3. **Legibilidad** → los métodos se llaman igual, aunque los objetos hagan cosas distintas.
    

Ejemplo más realista:

```javascript
class Pago {
  procesar(monto) {
    console.log("Procesando pago genérico de $" + monto);
  }
}

class PagoTarjeta extends Pago {
  procesar(monto) {
    console.log("Procesando pago con tarjeta de $" + monto);
  }
}

class PagoPaypal extends Pago {
  procesar(monto) {
    console.log("Procesando pago con PayPal de $" + monto);
  }
}

function ejecutarPago(pago, monto) {
  pago.procesar(monto);
}

ejecutarPago(new PagoTarjeta(), 1000);
// "Procesando pago con tarjeta de $1000"

ejecutarPago(new PagoPaypal(), 500);
// "Procesando pago con PayPal de $500"
```

🔎 El mismo método `procesar()` se adapta a distintos **medios de pago**, sin que tengamos que cambiar la función `ejecutarPago`.

---

## 🔹 Diagrama ilustrativo

```
        Clase Padre: Animal
                │
      ┌─────────┴─────────┐
      │                   │
   Perro               Gato
 hablar()            hablar()
 "Guau"              "Miau"

> Ambos comparten el mismo método (hablar),
  pero cada uno lo implementa a su manera.
```

---

## ✅ Resumen

- El **polimorfismo** es la capacidad de un mismo método de adoptar distintos comportamientos según el objeto.
    
- En JavaScript lo vemos de tres formas:
    
    1. **Sobrescritura** (clases hijas redefinen métodos del padre).
        
    2. **Sobrecarga simulada** (métodos con parámetros opcionales).
        
    3. **Duck Typing** (objetos que implementan el mismo método aunque no tengan relación entre sí).
        
- Nos permite escribir código **más flexible, escalable y reutilizable**.
    

---
