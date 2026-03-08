# 📌 Abstracción en Programación Orientada a Objetos

---

## 🔹 Definición General

La **abstracción** en POO es el proceso de **ocultar los detalles internos de implementación** de un objeto y **exponer solo lo esencial** para el uso externo.

En otras palabras, cuando usamos abstracción, **mostramos lo que hace un objeto, pero no necesariamente cómo lo hace internamente**.

👉 Ejemplo de la vida real:  
Cuando usamos un **control remoto de TV**, sabemos que presionar el botón _“encender”_ prende la televisión.

- Lo que **vemos**: botones fáciles de usar (interfaz).
    
- Lo que **no vemos**: circuitos eléctricos, señales infrarrojas, procesos internos (implementación).
    

Eso es **abstracción** → acceder a una funcionalidad sin preocuparnos por los detalles internos.

---

## 🔹 Abstracción en JavaScript

A diferencia de lenguajes como **Java** o **C#**, donde existen **clases abstractas** y **interfaces** nativas, en **JavaScript no hay abstracción formal**.

Sin embargo, podemos **simular la abstracción** mediante varias técnicas:

1. Uso de **clases base** que definen la interfaz (qué métodos deberían existir).
    
2. Uso de **métodos abstractos simulados** (que lanzan errores si no se implementan).
    
3. Uso de **interfaces contractuales** a través de convenciones (duck typing).
    
4. Uso de **módulos** o **encapsulamiento** para ocultar detalles.
    

---

## 🔹 Ejemplo 1: Clase base simulando abstracción

```js
class Figura {
  constructor() {
    if (this.constructor === Figura) {
      throw new Error("No se puede instanciar una clase abstracta");
    }
  }

  calcularArea() {
    throw new Error("Debes implementar el método calcularArea()");
  }
}

class Circulo extends Figura {
  constructor(radio) {
    super();
    this.radio = radio;
  }

  calcularArea() {
    return Math.PI * this.radio ** 2;
  }
}

class Rectangulo extends Figura {
  constructor(base, altura) {
    super();
    this.base = base;
    this.altura = altura;
  }

  calcularArea() {
    return this.base * this.altura;
  }
}

let c = new Circulo(5);
let r = new Rectangulo(4, 6);

console.log(c.calcularArea()); // 78.5398...
console.log(r.calcularArea()); // 24
```

---

### 📌 Explicación paso a paso

1. `Figura` es una **clase abstracta simulada**:
    
    - No se puede instanciar directamente (`new Figura()` lanza error).
        
    - Obliga a las subclases a implementar el método `calcularArea()`.
        
2. `Circulo` y `Rectangulo` **heredan de Figura** y deben implementar `calcularArea`.
    
    - Si no lo hacen → error.
        
    - Si lo hacen → cada clase calcula el área de manera distinta.
        
3. Desde el exterior (`c.calcularArea()` o `r.calcularArea()`), **sabemos qué hace cada objeto, pero no nos importa cómo lo hace**.
    

👉 Esto es **abstracción pura**: el usuario solo necesita saber que existe un método `calcularArea()`.

---

## 🔹 Ejemplo 2: Abstracción con Interfaces Simuladas (Duck Typing)

En JS no tenemos `interface`, pero podemos usar convenciones:

```js
function dibujarFigura(figura) {
  if (typeof figura.dibujar !== "function") {
    throw new Error("El objeto no implementa el método 'dibujar'");
  }
  figura.dibujar();
}

class Triangulo {
  dibujar() {
    console.log("Se dibuja un triángulo");
  }
}

class Estrella {
  dibujar() {
    console.log("Se dibuja una estrella");
  }
}

let t = new Triangulo();
let e = new Estrella();

dibujarFigura(t); // "Se dibuja un triángulo"
dibujarFigura(e); // "Se dibuja una estrella"
```

👉 Aquí la función `dibujarFigura` **no le importa el tipo exacto del objeto** (triángulo, estrella, etc.), solo le importa que **tenga el método `dibujar`**.  
Esto es **abstracción + duck typing**.

---

## 🔹 Ejemplo 3: Abstracción + Encapsulamiento

Podemos combinar abstracción y encapsulamiento para **ocultar detalles internos** y mostrar solo lo necesario:

```js
class Auto {
  #encendido = false; // atributo privado

  encender() {
    this.#encendido = true;
    console.log("El auto está encendido");
  }

  apagar() {
    this.#encendido = false;
    console.log("El auto está apagado");
  }

  estado() {
    return this.#encendido ? "Encendido" : "Apagado";
  }
}

let miAuto = new Auto();
miAuto.encender();      // "El auto está encendido"
console.log(miAuto.estado()); // "Encendido"
```

👉 El usuario de la clase `Auto` no sabe cómo internamente se maneja `#encendido`.  
Solo ve métodos simples: `encender()`, `apagar()` y `estado()`.  
Eso es **abstracción aplicada**.

---

## 🔹 Diagrama ilustrativo

```
   ┌───────────────────────┐
   │       Clase Figura     │  (Abstracta)
   │───────────────────────│
   │ + calcularArea()      │  <-- Método abstracto
   └──────────┬────────────┘
              │
   ┌──────────┴──────────┐
   │                     │
┌──▼───┐             ┌───▼───┐
│Círculo│             │Rectángulo│
│-------│             │----------│
│radio  │             │base,altura│
│+calcularArea()      │+calcularArea() │
└───────┘             └───────────┘
```

👉 `Figura` define la **interfaz común** (qué métodos deben existir).  
👉 `Círculo` y `Rectángulo` implementan sus **detalles internos** (cálculo del área).

---

## 🔑 Conclusión

- La **abstracción** en POO consiste en **mostrar solo lo esencial** y ocultar los detalles internos.
    
- En JavaScript no hay **clases abstractas** nativas, pero podemos **simularlas** mediante:
    
    - clases base con métodos que lanzan errores,
        
    - duck typing,
        
    - encapsulamiento y convención.
        
- La abstracción ayuda a **simplificar el uso de objetos complejos**, garantizando una interfaz clara y consistente.
    

---