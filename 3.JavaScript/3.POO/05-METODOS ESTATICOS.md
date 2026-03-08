# Métodos Estáticos en JavaScript

En la programación orientada a objetos, los métodos estáticos representan una categoría especial de funciones que pertenecen a la clase en sí, más que a sus instancias. En JavaScript, estos métodos se definen mediante la palabra clave `static` dentro de la clase. A diferencia de los métodos de instancia, que operan sobre los datos específicos de un objeto creado con `new`, los métodos estáticos no tienen acceso directo a las propiedades de instancia (`this`), sino que interactúan con la clase como entidad global.

El uso de métodos estáticos es particularmente relevante cuando se requiere implementar funcionalidades auxiliares, utilitarias o de carácter global, como operaciones matemáticas, contadores de instancias o validaciones que no dependen del estado particular de un objeto. Esta característica contribuye a una mejor organización del código, agrupando funcionalidades relacionadas bajo la clase correspondiente sin necesidad de crear objetos innecesarios.

---

## Ejemplo conceptual básico

```javascript
class Calculadora {
  static sumar(a, b) {
    return a + b;
  }

  static multiplicar(a, b) {
    return a * b;
  }
}

// Uso de métodos estáticos
console.log(Calculadora.sumar(4, 7));       // 11
console.log(Calculadora.multiplicar(3, 5)); // 15
```

En este ejemplo, `sumar` y `multiplicar` son métodos estáticos. Observamos que no requieren la creación de una instancia de `Calculadora` para ser utilizados. Cualquier intento de acceder a ellos desde un objeto creado con `new` resultaría en un valor `undefined`, ya que la propiedad no pertenece a la instancia sino a la clase.

---

## Métodos estáticos y herencia

La herencia en métodos estáticos permite que las clases derivadas puedan reutilizar la lógica definida en las clases base. Esta característica es consistente con la filosofía de la programación orientada a objetos de promover la reutilización y la extensión del código.

```javascript
class Animal {
  static info() {
    console.log("Todos los animales poseen vida.");
  }
}

class Perro extends Animal {
  static infoPerro() {
    console.log("Los perros son mamíferos.");
  }
}

Animal.info();       // "Todos los animales poseen vida."
Perro.info();        // Heredado: "Todos los animales poseen vida."
Perro.infoPerro();   // "Los perros son mamíferos."
```

En este contexto, la clase `Perro` hereda el método estático `info` de `Animal`, demostrando que los métodos estáticos pueden formar parte de la jerarquía de herencia y ser invocados directamente desde la subclase. Es posible además utilizar `super` dentro de un método estático para invocar la implementación del método en la clase padre, lo que facilita la extensión de la funcionalidad sin duplicación de código.

```javascript
class Gato extends Animal {
  static info() {
    super.info();
    console.log("Los gatos son felinos.");
  }
}

Gato.info();
// Salida:
// "Todos los animales poseen vida."
// "Los gatos son felinos."
```

---

## Consideraciones finales

El uso de métodos estáticos permite diferenciar claramente entre:

- Funcionalidades **ligadas a la clase**, que no dependen de ningún estado particular de sus instancias.
    
- Funcionalidades **ligadas a la instancia**, que operan sobre los datos propios de cada objeto.
    

De esta manera, los métodos estáticos se convierten en herramientas fundamentales para mantener un diseño claro, modular y coherente en la programación orientada a objetos en JavaScript, integrando conceptos de reutilización, abstracción y organización lógica del código.

---

