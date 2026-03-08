## 05 - Herencia

---

## 🔹 1. Introducción a la herencia

La **herencia** es un principio fundamental de la **Programación Orientada a Objetos (POO)** que permite que una **clase derivada (subclase)** adopte propiedades y métodos de otra **clase base (superclase)**.

- **Objetivo principal:** reutilizar código, evitando duplicaciones.
    
- **Beneficios:**
    
    1. **Reutilización de código:** La subclase hereda comportamientos ya implementados en la clase padre.
        
    2. **Jerarquía y organización:** Se pueden crear estructuras de clases que reflejen relaciones lógicas, por ejemplo `Animal → Mamífero → Perro`.
        
    3. **Mantenimiento más fácil:** Cambios en la clase padre se reflejan automáticamente en las subclases.
        

> ⚠️ Nota: la herencia no debe confundirse con **composición**, que consiste en crear objetos más complejos combinando otros objetos, en lugar de depender de jerarquías profundas.

---

## 🔹 2. Herencia en JavaScript: enfoque histórico

Antes de ES6, JavaScript no tenía clases nativas. Se usaban **funciones constructoras** y **prototipos** para simular la herencia.

### 🔹 Ejemplo 1: Función constructora + prototipo

```js
// Clase padre simulada
function Animal(nombre) {
  this.nombre = nombre;
}

Animal.prototype.saludar = function() {
  console.log(`Hola, soy ${this.nombre}`);
};

// Subclase simulada
function Perro(nombre, raza) {
  Animal.call(this, nombre); // hereda propiedades
  this.raza = raza;
}

// Heredar métodos del prototipo de Animal
Perro.prototype = Object.create(Animal.prototype);
Perro.prototype.constructor = Perro;

// Método propio de la subclase
Perro.prototype.ladrar = function() {
  console.log(`${this.nombre} ladra: ¡Guau!`);
};

let perro1 = new Perro("Firulais", "Labrador");
perro1.saludar(); // "Hola, soy Firulais"
perro1.ladrar();  // "Firulais ladra: ¡Guau!"
```

**Explicación:**

- `Animal.call(this, nombre)` permite **heredar las propiedades** del padre.
    
- `Object.create(Animal.prototype)` permite que **los métodos del padre** se hereden.
    
- `Perro.prototype.constructor = Perro` asegura que el constructor de la subclase sea correcto.
    
- Aquí vemos claramente la **simulación de herencia** usando funciones constructoras y prototipos.
    

> ✅ Limitación: La sintaxis es menos clara y más propensa a errores que las clases modernas.

---

## 🔹 3. Herencia con clases modernas (`class` + `extends`)

Con ES6, JavaScript introdujo la sintaxis de **clases** para simplificar y hacer más legible la herencia.

### 🔹 Ejemplo 2: Clases modernas

```js
class Animal {
  constructor(nombre) {
    this.nombre = nombre;
  }

  saludar() {
    console.log(`Hola, soy ${this.nombre}`);
  }
}

class Perro extends Animal {
  constructor(nombre, raza) {
    super(nombre); // Llama al constructor del padre
    this.raza = raza;
  }

  ladrar() {
    console.log(`${this.nombre} ladra: ¡Guau!`);
  }
}

let perro2 = new Perro("Max", "Beagle");
perro2.saludar(); // "Hola, soy Max"
perro2.ladrar();  // "Max ladra: ¡Guau!"
```

**Explicación:**

- `extends` indica que `Perro` hereda de `Animal`.
    
- `super(nombre)` llama al **constructor de la clase padre**, necesario para inicializar las propiedades heredadas.
    
- Los métodos de la clase padre (`saludar`) se **heredan automáticamente**, mientras que los métodos propios (`ladrar`) se agregan solo a la subclase.
    
- Esta sintaxis es más clara y moderna que la basada en prototipos.
    

---

## 🔹 4. Sobrescritura de métodos (Polimorfismo parcial)

Una subclase puede **sobrescribir un método** de la clase padre para adaptarlo a su comportamiento específico.

### 🔹 Ejemplo 3: Sobrescritura de métodos

```js
class Personaje {
  atacar() {
    console.log("El personaje ataca con fuerza física.");
  }
}

class Mago extends Personaje {
  atacar() {
    console.log("El mago lanza un hechizo mágico.");
  }
}

let p = new Personaje();
p.atacar(); // "El personaje ataca con fuerza física."

let m = new Mago();
m.atacar(); // "El mago lanza un hechizo mágico."
```

**Explicación:**

- `Mago` **hereda** de `Personaje`, pero sobrescribe el método `atacar()`.
    
- Esto es una forma de **polimorfismo**, porque el mismo método (`atacar`) se comporta diferente según la instancia.
    

---

## 🔹 5. Buenas prácticas en herencia

1. **Evitar jerarquías profundas**: demasiadas capas dificultan mantenimiento.
    
2. **Clase padre genérica**: que se pueda reutilizar y no dependa de detalles muy específicos de la subclase.
    
3. **Evitar duplicar métodos**: si se repite código, debería ir en la clase padre.
    
4. **Usar composición cuando sea más lógico**: si un objeto necesita muchas funcionalidades independientes, a veces es mejor combinar objetos en lugar de heredar.
    

---

## 🔹 6. Ejemplo práctico completo: antiguo vs moderno

### Antiguo (funciones constructoras):

```js
function Vehiculo(tipo) {
  this.tipo = tipo;
}

Vehiculo.prototype.mover = function() {
  console.log(`${this.tipo} se mueve.`);
};

function Auto(tipo, marca) {
  Vehiculo.call(this, tipo);
  this.marca = marca;
}

Auto.prototype = Object.create(Vehiculo.prototype);
Auto.prototype.constructor = Auto;

Auto.prototype.mover = function() {
  console.log(`${this.marca} se mueve rápidamente.`);
};

let auto1 = new Auto("Coche", "Toyota");
auto1.mover(); // "Toyota se mueve rápidamente."
```

### Moderno (clases ES6):

```js
class Vehiculo {
  constructor(tipo) {
    this.tipo = tipo;
  }

  mover() {
    console.log(`${this.tipo} se mueve.`);
  }
}

class Auto extends Vehiculo {
  constructor(tipo, marca) {
    super(tipo);
    this.marca = marca;
  }

  mover() {
    console.log(`${this.marca} se mueve rápidamente.`);
  }
}

let auto2 = new Auto("Coche", "Toyota");
auto2.mover(); // "Toyota se mueve rápidamente."
```

**Comparación:**

- La versión moderna es **más clara y fácil de leer**.
    
- Heredar y sobrescribir métodos es directo, sin necesidad de `Object.create` ni `call`.
    

---

## 📌 Conclusión

- La **herencia** permite que las subclases reutilicen propiedades y métodos de la clase padre.
    
- En JavaScript:
    
    - Antes de ES6 → funciones constructoras + prototipos (`Object.create`, `call`).
        
    - Desde ES6 → clases modernas (`class` + `extends` + `super`).
        
- La **sobrescritura de métodos** permite adaptar comportamientos específicos en subclases.
    
- Es recomendable usar herencia **cuando existe una relación “es un tipo de”**, y considerar **composición** cuando los objetos necesitan múltiples funcionalidades independientes.
    

---

