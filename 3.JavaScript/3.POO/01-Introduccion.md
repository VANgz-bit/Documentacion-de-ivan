
---

# 📂 01 - Introducción a la POO en JavaScript

---

## 🔹 ¿Qué es la POO?

La **Programación Orientada a Objetos (POO)** es un **paradigma de programación**, es decir, una manera de pensar y organizar el código.  
Se basa en la idea de que podemos modelar los elementos de un problema como **objetos** que representan entidades del mundo real o abstracto.

Un **objeto** en este contexto es una **unidad que combina datos y comportamientos**:

- Los **datos** se representan como **propiedades** o **atributos**.
    
- Los **comportamientos** se representan como **métodos** o **funciones** asociadas al objeto.
    

Esto permite que el código se sienta más cercano al lenguaje natural. Por ejemplo, en lugar de tener una lista de funciones sueltas como `mover(personaje)`, `atacar(personaje)`, podemos tener un objeto `Personaje` con métodos `mover()` y `atacar()`.

👉 En resumen: la POO busca que los programas estén compuestos por **objetos que interactúan entre sí**, como si fueran piezas de un sistema más grande.

---

## 🔹 ¿Por qué usar POO?

La POO trae varias **ventajas importantes** frente a la programación estructurada (la que se basa solo en funciones y datos separados):

1. **Organización** → el código se estructura en objetos que agrupan todo lo relacionado.
    
2. **Reutilización** → se pueden crear moldes (clases) y luego generar múltiples instancias sin repetir código.
    
3. **Escalabilidad** → es más fácil ampliar o modificar un sistema grande.
    
4. **Mantenibilidad** → al tener el código dividido en entidades más claras, se entiende y corrige más rápido.
    
5. **Correspondencia con el mundo real** → se pueden modelar personajes, autos, usuarios, productos, etc., como objetos con atributos y acciones.
    

---

## 🔹 Pilares de la POO

La POO se apoya en **cuatro pilares fundamentales**. Estos los estudiaremos en secciones específicas, pero aquí los presentamos a modo de introducción:

1. **Encapsulamiento**
    
    - Consiste en **ocultar los detalles internos** de un objeto y exponer solo lo necesario.
        
    - Permite controlar cómo se accede y modifica la información.
        
    - En JavaScript moderno se logra con propiedades privadas (`#atributo`), y con `getters` y `setters`.
        
2. **Herencia**
    
    - Permite que una clase “hija” adquiera propiedades y métodos de una clase “padre”.
        
    - Favorece la **reutilización de código** y la creación de jerarquías.
        
3. **Polimorfismo**
    
    - Significa que un mismo método puede tener **distintos comportamientos** según el objeto que lo use.
        
    - Ejemplo: un método `hacerSonido()` puede devolver “Guau” en un perro y “Miau” en un gato.
        
4. **Abstracción**
    
    - Es la capacidad de crear **modelos generales** que sirven como base para casos concretos.
        
    - Se enfoca en lo esencial, ignorando los detalles que no son relevantes en ese nivel.
        

👉 Estos cuatro pilares hacen que la POO sea flexible y poderosa.

---

## 🔹 Objetos en JavaScript

En JavaScript, un objeto es una **estructura dinámica de pares clave–valor**.  
Las **claves** (keys) suelen ser strings o symbols, y los **valores** pueden ser de cualquier tipo (números, strings, booleanos, funciones, otros objetos, etc.).

### Ejemplo simple: objeto literal

```js
let personaje = {
  nombre: "Arthas",
  nacion: "Lordaeron",
  poder: "controlar a los muertos",
  presentarse: function() {
    console.log(`Soy ${this.nombre} y puedo ${this.poder}`);
  }
};

personaje.presentarse();
// Soy Arthas y puedo controlar a los muertos
```

👉 Aquí creamos un **objeto literal**, es decir, directamente con llaves `{}`.  
Esto es muy útil para un objeto único, pero si quisiéramos crear **cientos de personajes distintos**, se volvería repetitivo y difícil de mantener.

> IMPORTANTE: los objetos en js ya fueron detallados en su seccion de tipos de datos > objetos.

---

## 🔹 El sistema de prototipos en JavaScript

A diferencia de lenguajes como Java o C#, JavaScript **no nació con clases tradicionales**.  
Su sistema se basa en los **prototipos**.

- Todo objeto tiene un enlace interno llamado **`[[Prototype]]`**, que apunta a otro objeto.
    
- Ese otro objeto es su **prototipo**, que funciona como “herencia por delegación”.
    
- Si un objeto no encuentra una propiedad en sí mismo, la busca en su prototipo, y así sucesivamente (cadena de prototipos).
    

### Ejemplo:

```js
let heroe = { nombre: "Link" };

console.log(heroe.toString());
// Aunque no definimos toString en "heroe",
// funciona porque lo hereda de Object.prototype
```

👉 Esto demuestra que muchos métodos de JS no viven en el objeto en sí, sino en su **prototipo base** (`Object.prototype`).

---

## 🔹 Funciones constructoras

Antes de ES6, para crear múltiples objetos similares se usaban **funciones constructoras**.

Una **función constructora** es simplemente una función que se llama con `new`.

- `new` crea un objeto vacío.
    
- Ese objeto enlaza su `[[Prototype]]` al `prototype` de la función.
    
- Luego ejecuta la función, asignando propiedades con `this`.
    

### Ejemplo:

```js
function Personaje(nombre, nacion, poder) {
  this.nombre = nombre;
  this.nacion = nacion;
  this.poder = poder;
}

let pj1 = new Personaje("Arthas", "Lordaeron", "controlar a los muertos");
console.log(pj1.nombre); // Arthas
```

👉 Aquí `Personaje` es un **molde** para crear personajes.

---

## 🔹 Métodos en el prototype

Para que las funciones no se repitan en cada objeto, se usaba el objeto especial `prototype`.

### Ejemplo:

```js
Personaje.prototype.presentarse = function() {
  console.log(`Soy ${this.nombre} de ${this.nacion}, puedo ${this.poder}`);
};

pj1.presentarse();
// Soy Arthas de Lordaeron, puedo controlar a los muertos
```

👉 De este modo, todas las instancias de `Personaje` comparten un único método `presentarse` en memoria.

---

## 🔹 Clases ES6 (azúcar sintáctica)

Con ES6 llegó la sintaxis `class`, que luce más clara y moderna, pero internamente sigue funcionando con prototipos.

### Ejemplo equivalente:

```js
class Personaje {
  constructor(nombre, nacion, poder) {
    this.nombre = nombre;
    this.nacion = nacion;
    this.poder = poder;
  }

  presentarse() {
    console.log(`Soy ${this.nombre} de ${this.nacion}, puedo ${this.poder}`);
  }
}

let pj2 = new Personaje("Illidan", "Outland", "usar magia demoníaca");
pj2.presentarse();
// Soy Illidan de Outland, puedo usar magia demoníaca
```

👉 Aquí parece “magia”, pero en realidad JavaScript sigue creando un prototipo detrás de escena.


---

## 🔹 Conexión entre prototipos y clases

Es muy importante aclarar:

- **Las clases no reemplazaron los prototipos**:  
    son solo **azúcar sintáctica** que hace más cómodo trabajar con ellos.
    
- Internamente, la clase anterior se traduce a algo equivalente a:
    
    - Una función constructora.
        
    - Un objeto `prototype` con los métodos de la clase.
        

### Ejemplo detrás de escena:

```js
console.log(typeof Personaje); // function
console.log(Personaje.prototype.presentarse); // [Function: presentarse]
```

👉 Aunque usamos `class`, JS lo interpreta como una **función constructora con un prototipo asociado**.

---

## 🔹 Conclusión de la introducción

- La POO organiza el código en objetos con propiedades y métodos.
    
- En JS, todo parte de los **objetos y prototipos**.
    
- Antes de ES6, se usaban **funciones constructoras + prototype**.
    
- Con ES6 se introdujeron las **clases**, que son azúcar sintáctica sobre los prototipos.
    
- Entender los prototipos es clave para comprender cómo funcionan las clases en realidad.
    

👉 A partir de aquí, trabajaremos con **clases** para explicar los pilares de la POO (encapsulamiento, herencia, polimorfismo y abstracción).

---

