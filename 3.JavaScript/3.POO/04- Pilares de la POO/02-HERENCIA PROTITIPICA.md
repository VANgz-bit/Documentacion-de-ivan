# 📖 Herencia Prototípica en JavaScript

---

## 🔹 Introducción al concepto

En JavaScript, la herencia no funciona como en lenguajes puramente orientados a clases (Java, C++, C#). En lugar de depender de clases rígidas, **cada objeto puede servir como modelo o base para otros objetos**. A esto lo llamamos **herencia prototípica**.

Un **prototipo** no es más que un **objeto especial** del cual otro objeto hereda propiedades y métodos. Esta relación forma una cadena llamada **Prototype Chain (cadena de prototipos)**, que JavaScript utiliza automáticamente para resolver búsquedas de propiedades.

👉 Esto significa que **todas las instancias y objetos en JavaScript se construyen a partir de otros objetos**. Incluso si definimos una clase, en el fondo sigue siendo azúcar sintáctica para manejar prototipos.

---

## 🔹 ¿Qué es un prototipo?

Un **prototipo** es un **objeto asociado internamente** a otro objeto. Su misión principal es **compartir propiedades y métodos** entre múltiples objetos sin necesidad de duplicarlos en cada instancia.

Cada objeto en JavaScript tiene una referencia interna llamada `[[Prototype]]`, que apunta a su prototipo. Aunque no accedemos directamente a `[[Prototype]]`, sí podemos consultarlo mediante:

- `Object.getPrototypeOf(obj)` → forma recomendada.
    
- `obj.__proto__` → atajo no estándar pero ampliamente soportado.
    

🔎 **Ejemplo introductorio**:

```javascript
let persona = {
  saludar: function() {
    console.log("Hola, soy una persona.");
  }
};

let juan = Object.create(persona);
juan.nombre = "Juan";

console.log(juan.nombre); // "Juan" (propiedad propia de juan)
juan.saludar();           // "Hola, soy una persona." (heredado de persona)
```

📌 **Explicación paso a paso**:

1. Creamos `persona`, un objeto que contiene el método `saludar`.
    
2. Luego usamos `Object.create(persona)` para crear `juan`. Esto hace que `juan` tenga como prototipo a `persona`.
    
3. Cuando pedimos `juan.saludar()`, el motor de JS no lo encuentra directamente en `juan`, así que **sube al prototipo** y lo encuentra en `persona`.
    

---

## 🔹 La cadena de prototipos (Prototype Chain)

La **Prototype Chain** es el mecanismo que usa JavaScript para buscar propiedades y métodos.  
El proceso es el siguiente:

1. Busca la propiedad en el propio objeto.
    
2. Si no está, busca en su prototipo (`[[Prototype]]`).
    
3. Si no la encuentra, sigue subiendo en la cadena hasta llegar a `Object.prototype`.
    
4. Si no existe en ningún nivel, devuelve `undefined`.
    

🔎 **Ejemplo con animales**:

```javascript
let animal = {
  respirar: function() {
    console.log("El animal respira.");
  }
};

let perro = Object.create(animal);
perro.ladrar = function() {
  console.log("El perro ladra.");
};

perro.ladrar();   // "El perro ladra." (definido en perro)
perro.respirar(); // "El animal respira." (heredado de animal)
```

📌 **Explicación**:

- `perro` tiene su propio método `ladrar`.
    
- Como `respirar` no está definido en `perro`, el motor de JS lo busca en su prototipo (`animal`) y lo encuentra allí.
    
- Si no lo encontrara en `animal`, seguiría hasta `Object.prototype`, que contiene métodos universales como `toString()` o `hasOwnProperty()`.
    

---

## 🔹 Diagrama de la cadena de prototipos

Así podríamos representar gráficamente la relación de herencia:

```
perro ---> { ladrar() }
   |
   v
[[Prototype]] ---> animal ---> { respirar() }
                         |
                         v
             [[Prototype]] ---> Object.prototype ---> { toString(), hasOwnProperty(), ... }
                                                |
                                                v
                                               null

```

👉 Observa que todos los caminos terminan en `Object.prototype`, que es el **último eslabón común de la cadena**.

---

## 🔹 Funciones constructoras y herencia prototípica

Antes de ES6 y las `class`, la forma de simular herencia era mediante **funciones constructoras** combinadas con la manipulación manual de prototipos.

🔎 **Ejemplo clásico**:

```javascript
function Animal(nombre) {
  this.nombre = nombre;
}

Animal.prototype.respirar = function() {
  console.log(this.nombre + " está respirando.");
};

function Perro(nombre, raza) {
  // Llamamos al constructor padre para inicializar nombre
  Animal.call(this, nombre);  
  this.raza = raza;
}

// Establecer la relación de herencia
Perro.prototype = Object.create(Animal.prototype);

// Corregir el constructor
Perro.prototype.constructor = Perro;

// Método propio de Perro
Perro.prototype.ladrar = function() {
  console.log(this.nombre + " está ladrando.");
};

let miPerro = new Perro("Firulais", "Labrador");

miPerro.respirar(); // "Firulais está respirando."
miPerro.ladrar();   // "Firulais está ladrando."
```

📌 **Explicación detallada**:

1. `Animal` actúa como **función constructora base**.
    
2. Su prototipo (`Animal.prototype`) contiene el método `respirar`.
    
3. `Perro` es otra función constructora, que llama a `Animal.call(this, nombre)` para heredar propiedades de instancia (como `nombre`).
    
4. Con `Perro.prototype = Object.create(Animal.prototype)` conectamos la cadena de prototipos.
    
5. Como reasignamos el `prototype`, corregimos la referencia de `constructor`.
    
6. Finalmente, `Perro.prototype.ladrar` define un método exclusivo para perros.
    

---

## 🔹 Herencia con clases modernas (ES6)

Con la llegada de ES6, JavaScript introdujo `class` y `extends`.  
En realidad, no cambió el modelo de herencia: **debajo sigue funcionando con prototipos**, pero la sintaxis es más limpia y clara.

🔎 **Ejemplo equivalente con clases**:

```javascript
class Animal {
  constructor(nombre) {
    this.nombre = nombre;
  }

  respirar() {
    console.log(this.nombre + " está respirando.");
  }
}

class Perro extends Animal {
  constructor(nombre, raza) {
    super(nombre); // Llama al constructor de Animal
    this.raza = raza;
  }

  ladrar() {
    console.log(this.nombre + " está ladrando.");
  }
}

let miPerro = new Perro("Firulais", "Labrador");

miPerro.respirar(); // "Firulais está respirando."
miPerro.ladrar();   // "Firulais está ladrando."
```

📌 **Explicación**:

- `extends` establece la herencia de manera explícita.
    
- `super(nombre)` invoca al constructor de la clase padre (similar a `Animal.call(this, nombre)`).
    
- La **prototype chain** sigue existiendo, solo que ahora no necesitamos configurarla manualmente.
    

---

##  Resumen

- **Herencia prototípica**: mecanismo base de herencia en JavaScript.
    
- Todos los objetos tienen un **prototipo**, que forma parte de la **Prototype Chain**.
    
- Antes de ES6 se usaban **funciones constructoras** y manipulación manual de prototipos (`Object.create`, `.call()`).
    
- Con **clases y `extends`**, se introdujo una sintaxis más clara y legible, aunque debajo sigue funcionando con prototipos.
    
- Entender la **Prototype Chain** es clave para comprender cómo funciona **toda la herencia en JavaScript**.
    

---
