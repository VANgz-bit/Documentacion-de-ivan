# 📂 02 - Clases y Objetos

La **Programación Orientada a Objetos (POO)** en JavaScript se fundamenta en la idea de que podemos modelar conceptos del mundo real o abstracto mediante **objetos** que poseen **características** (propiedades) y **comportamientos** (métodos).  
Dentro de este paradigma, una **clase** funciona como un **molde** o **plantilla** que nos permite definir cómo deben construirse esos objetos.

Antes de la llegada de **ES6 (2015)**, JavaScript utilizaba **funciones constructoras** y el mecanismo de los **prototipos** para crear objetos con una estructura compartida. Ese enfoque sigue existiendo en el motor del lenguaje, pero la sintaxis `class` fue introducida para hacer este proceso más **claro, legible y cercano a otros lenguajes** como Java, Python o C++.

Podemos pensar a las clases como **recetas**. Una receta define qué ingredientes y pasos hacen falta para preparar un plato, pero hasta que no cocinamos siguiendo esa receta, no tenemos un plato real. De igual forma, una clase define la estructura y el comportamiento de los objetos, pero hasta que no **instanciamos** la clase, no tenemos un objeto concreto en memoria.

---

## La definición de una clase

En JavaScript, una clase se define con la palabra reservada `class` seguida de un nombre (por convención, se escribe en **PascalCase**, es decir, con la primera letra en mayúscula).

Dentro de la clase podemos encontrar principalmente dos elementos:

- El **constructor**, que es un método especial encargado de inicializar las propiedades del objeto en el momento en que se crea.
    
- Los **métodos de instancia**, que son las acciones que ese objeto podrá ejecutar.
    

Veamos un ejemplo sencillo:

```js
class Personaje {
  // El constructor recibe parámetros y define las propiedades iniciales
  constructor(nombre, nacion, genero, poder) {
    this.nombre = nombre;   // this hace referencia al objeto actual
    this.nacion = nacion;
    this.genero = genero;
    this.poder = poder;
  }

  // Método: comportamiento del objeto
  presentarse() {
    console.log(
      `Soy ${this.nombre}, provengo de ${this.nacion} y mi habilidad es ${this.poder}.`
    );
  }
}
```

En este código hemos definido una clase llamada `Personaje`. Dentro de ella:

- El **constructor** asigna valores iniciales a las propiedades `nombre`, `nacion`, `genero` y `poder`.
    
- El método `presentarse()` imprime un mensaje con esos datos.
    

---

## La creación de objetos (instancias)

Una clase, por sí misma, no produce nada concreto: es solo el molde. Para obtener un objeto real debemos **instanciarla** utilizando la palabra clave `new`. Cada vez que usamos `new`, se ejecuta el `constructor` de la clase y se crea un nuevo objeto en memoria con las características definidas.

```js
let personaje1 = new Personaje("Aiden", "Lumina", "Masculino", "controlar el fuego");
let personaje2 = new Personaje("Selene", "Noctis", "Femenino", "manipular las sombras");

personaje1.presentarse(); 
// → Soy Aiden, provengo de Lumina y mi habilidad es controlar el fuego.

personaje2.presentarse(); 
// → Soy Selene, provengo de Noctis y mi habilidad es manipular las sombras.
```

Aquí podemos observar lo siguiente:

- **`personaje1`** y **`personaje2`** son dos objetos distintos, cada uno con datos propios.
    
- Ambos comparten la misma **estructura y comportamiento**, porque provienen de la misma clase.
    
- Cuando llamamos al método `presentarse()`, el mensaje cambia según los valores de cada instancia.
    

Esto ilustra la diferencia esencial entre una clase y un objeto:

- La **clase** es el molde abstracto.
    
- El **objeto** (o instancia) es el resultado concreto creado a partir de ese molde.
    

---

## El rol del `this`

Dentro de una clase, la palabra clave `this` hace referencia al **objeto que está siendo creado o que está ejecutando un método en ese momento**.

En el constructor, `this.nombre = nombre` significa “la propiedad `nombre` de este objeto será igual al valor recibido como parámetro `nombre`”.  
En el método `presentarse()`, `this.nombre` busca el valor dentro de la instancia que invocó al método.

Esto asegura que cada objeto maneje sus propios datos, aunque todos provengan de la misma clase.

---

## Clases y prototipos: lo que ocurre detrás de escena

Aunque la sintaxis de clases es nueva, lo que ocurre internamente sigue siendo el modelo de **prototipos** de JavaScript.  
Cuando definimos un método dentro de una clase, en realidad ese método se añade al **prototype** de la clase, y todas las instancias lo comparten.

Esto significa que el código:

```js
class Personaje {
  presentarse() {
    console.log("Hola");
  }
}
```

es equivalente a:

```js
function Personaje() {}
Personaje.prototype.presentarse = function () {
  console.log("Hola");
};
```

La diferencia es que la sintaxis `class` resulta mucho más legible y menos propensa a errores.

---

## Ventajas de usar clases

1. **Organización**: el código se agrupa de manera lógica (propiedades en el constructor, métodos en la clase).
    
2. **Reutilización**: podemos crear múltiples objetos con la misma estructura sin repetir código.
    
3. **Escalabilidad**: facilitan la construcción de programas grandes y mantenibles.
    
4. **Legibilidad**: la sintaxis es más clara que las funciones constructoras y prototipos manuales.
    

---

## Ejemplo práctico ampliado

Supongamos que queremos crear un mini sistema de personajes para un juego. Definimos nuestra clase `Personaje` y generamos varios héroes y villanos:

```js
class Personaje {
  constructor(nombre, nacion, genero, poder) {
    this.nombre = nombre;
    this.nacion = nacion;
    this.genero = genero;
    this.poder = poder;
  }

  presentarse() {
    console.log(
      `Soy ${this.nombre}, de ${this.nacion}. Mi poder es ${this.poder}.`
    );
  }

  atacar(objetivo) {
    console.log(`${this.nombre} ataca a ${objetivo} usando ${this.poder}.`);
  }
}

let heroe = new Personaje("Liora", "Solaria", "Femenino", "curar a los aliados");
let villano = new Personaje("Drax", "Umbra", "Masculino", "absorber energía vital");

heroe.presentarse(); 
// → Soy Liora, de Solaria. Mi poder es curar a los aliados.

villano.presentarse(); 
// → Soy Drax, de Umbra. Mi poder es absorber energía vital.

villano.atacar("Liora"); 
// → Drax ataca a Liora usando absorber energía vital.
```

En este ejemplo hemos visto:

- Cómo crear múltiples instancias de una misma clase.
    
- Cómo cada objeto mantiene sus datos únicos pero comparte los mismos métodos.
    
- Cómo extender el comportamiento de la clase añadiendo más métodos (`atacar`).
    

---

## Conclusión

El concepto de **clases y objetos** constituye la base de la Programación Orientada a Objetos en JavaScript. Las clases definen la estructura general y los métodos que todos los objetos de un mismo tipo compartirán, mientras que cada instancia generada con `new` tiene su propia identidad y valores particulares.

Aunque detrás de escena JavaScript sigue utilizando el sistema de prototipos, las clases nos ofrecen una sintaxis mucho más clara, legible y cercana a la forma en que otros lenguajes orientados a objetos trabajan.  
Este entendimiento nos prepara para profundizar en el siguiente tema: **el encapsulamiento**, donde veremos cómo controlar el acceso y la visibilidad de las propiedades y métodos de los objetos.

---
