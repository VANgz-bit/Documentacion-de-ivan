# 📂 03 - Métodos en POO (JavaScript)

## 🔹 ¿Qué es un método?

Un **método** es una función que está asociada a un objeto o a una clase. A diferencia de una función común, el método suele actuar **sobre los datos internos del objeto** al que pertenece, accediendo a ellos mediante la palabra clave `this`.

En programación orientada a objetos, los métodos son los que **definen el comportamiento** de las instancias, es decir, lo que un objeto **puede hacer**.

👉 **Ejemplo conceptual:**

- Una clase `Auto` puede tener propiedades como `marca`, `modelo` y `color`.
    
- Sus métodos serían acciones como `acelerar()`, `frenar()` o `tocarBocina()`.
    

---

## 🔹 Métodos en objetos literales

Antes de que existieran las clases en JavaScript, los objetos literales podían tener métodos definidos como pares **clave–valor** donde el valor es una función.

```js
let persona = {
  nombre: "Ana",
  saludar: function() {
    console.log(`Hola, soy ${this.nombre}`);
  }
};

persona.saludar(); // "Hola, soy Ana"
```

Desde ES6, se simplificó la sintaxis:

```js
let persona = {
  nombre: "Ana",
  saludar() { // ya no hace falta "function"
    console.log(`Hola, soy ${this.nombre}`);
  }
};

persona.saludar(); // "Hola, soy Ana"
```

---

## 🔹 Métodos en funciones constructoras y prototipos

Antes de las clases modernas, se usaban **funciones constructoras** para crear objetos. Los métodos se añadían al prototipo para que todas las instancias los compartieran (ahorrando memoria).

```js
function Animal(nombre) {
  this.nombre = nombre;
}

// Método en el prototipo
Animal.prototype.hablar = function() {
  console.log(`${this.nombre} hace un sonido.`);
};

let perro = new Animal("Firulais");
perro.hablar(); // "Firulais hace un sonido."
```

👉 Aquí vemos que `hablar` es un **método compartido**: no se copia en cada objeto, sino que vive en `Animal.prototype`.

---

## 🔹 Métodos en clases modernas

Con ES6, JavaScript incorporó la sintaxis de **clases**, que internamente siguen usando prototipos, pero de forma más clara y legible.

```js
class Animal {
  constructor(nombre) {
    this.nombre = nombre;
  }

  // Método de instancia
  hablar() {
    console.log(`${this.nombre} hace un sonido.`);
  }
}

let gato = new Animal("Michi");
gato.hablar(); // "Michi hace un sonido."
```

👉 Aquí el método `hablar` es equivalente al del ejemplo con `prototype`, solo que ahora está escrito dentro de la clase.

---

## 🔹 Tipos de métodos en clases

### 1. Métodos de instancia

Son los que se declaran dentro de la clase **sin usar ninguna palabra clave extra**. Se acceden a través de las instancias.

```js
class Calculadora {
  sumar(a, b) {
    return a + b;
  }
}

let calc = new Calculadora();
console.log(calc.sumar(2, 3)); // 5
```

---

### 2. Métodos estáticos (`static`)

Son métodos asociados a la **clase en sí misma**, no a sus instancias. Se usan para utilidades generales.

```js
class Utilidades {
  static generarID() {
    return Math.floor(Math.random() * 1000);
  }
}

console.log(Utilidades.generarID()); // Ej: 437
```

👉 Notar que no se hace `new Utilidades()`. Los métodos estáticos se llaman directamente desde la clase.

---

### 3. Getters y setters

Son métodos especiales que **simulan propiedades**.

- `get`: permite obtener un valor como si fuera una propiedad.
    
- `set`: permite modificarlo controlando la asignación.
    

```js
class Usuario {
  constructor(nombre) {
    this._nombre = nombre;
  }

  get nombre() {
    return this._nombre.toUpperCase();
  }

  set nombre(nuevo) {
    if (nuevo.length > 2) {
      this._nombre = nuevo;
    } else {
      console.log("Nombre demasiado corto");
    }
  }
}

let u = new Usuario("Ana");
console.log(u.nombre); // "ANA"

u.nombre = "Lu";       // "Nombre demasiado corto"
u.nombre = "Lucía";    
console.log(u.nombre); // "LUCÍA"
```

---

## 🔹 Métodos heredados y sobrescritos

Los métodos definidos en una clase padre se heredan automáticamente en la subclase.

```js
class Persona {
  saludar() {
    console.log("Hola!");
  }
}

class Estudiante extends Persona {
  saludar() {
    console.log("Hola, soy estudiante.");
  }
}

let e = new Estudiante();
e.saludar(); // "Hola, soy estudiante."
```

Aquí la subclase **sobrescribe** el método heredado → esto conecta directamente con el **polimorfismo**, que veremos en otro capítulo.

---

# 📌 Conclusión

- Los **métodos** definen el **comportamiento** de los objetos.
    
- Evolucionaron en JavaScript desde **funciones dentro de objetos literales** → **prototipos con funciones constructoras** → **clases modernas con métodos más claros**.
    
- Existen distintos tipos: **de instancia, estáticos, getters y setters**.
    
- Gracias a la herencia, los métodos se pueden **transmitir** y **sobrescribir**, lo cual abre la puerta al polimorfismo.
    

---
