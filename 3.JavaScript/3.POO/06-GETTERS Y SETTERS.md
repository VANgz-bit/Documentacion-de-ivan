# 📖 Getters y Setters en JavaScript

---

## 🔹 Introducción al concepto

En la **Programación Orientada a Objetos (POO)**, uno de los pilares fundamentales es el **encapsulamiento**, es decir, la capacidad de ocultar los detalles internos de un objeto y exponer solo lo necesario.

Para lograr esto, muchos lenguajes de programación (como Java, C# o Python) ofrecen mecanismos especiales para acceder y modificar los atributos de un objeto de manera **controlada**: los **métodos accesores** (`get`) y los **métodos modificadores** (`set`).

En JavaScript, estos mecanismos existen y se conocen como **getters** y **setters**.

- Un **getter** es un método especial que permite **obtener el valor de una propiedad privada o protegida**, pero sin acceder directamente a ella.
    
- Un **setter** es un método especial que permite **modificar el valor de una propiedad**, aplicando validaciones o restricciones antes de asignarla.
    

En otras palabras:

- **Getter → leer un valor de forma segura.**
    
- **Setter → escribir un valor de forma controlada.**
    

---

## 🔹 ¿Por qué usar getters y setters en lugar de acceder directamente?

Podría parecer más simple hacer algo como:

```javascript
class Usuario {
  constructor(nombre, password) {
    this.nombre = nombre;
    this.password = password;
  }
}

let u = new Usuario("Iván", "123456");
console.log(u.password);  // Acceso directo
u.password = "qwerty";    // Modificación directa
```

Esto funciona, pero **no hay control**: cualquier código externo puede cambiar el valor de `password` sin validaciones, incluso a un valor vacío o inseguro.

Con **getters y setters**, podemos:

- **Ocultar** el valor real.
    
- **Proteger** contra asignaciones indebidas.
    
- **Aplicar reglas de negocio** (ejemplo: una contraseña debe tener mínimo 6 caracteres).
    
- **Simular propiedades calculadas** (ejemplo: mostrar la edad a partir de la fecha de nacimiento).
    

---

## 🔹 Sintaxis básica de getters y setters en JavaScript

En JavaScript se usan las palabras reservadas `get` y `set` dentro de una clase u objeto literal.

### Ejemplo 1: Getter y Setter básicos

```javascript
class Usuario {
  #password; // propiedad privada

  constructor(nombre, password) {
    this.nombre = nombre;
    this.#password = password;
  }

  // Getter: no muestra la clave real
  get password() {
    return "*****";
  }

  // Setter: valida antes de asignar
  set password(nuevaClave) {
    if (nuevaClave.length >= 6) {
      this.#password = nuevaClave;
    } else {
      console.log("La clave es demasiado corta");
    }
  }

  autenticar(clave) {
    return this.#password === clave;
  }
}

// Uso
let u = new Usuario("Iván", "123456");

console.log(u.password);      // "*****" → accedemos al getter
u.password = "abc";           // Setter → "La clave es demasiado corta"
u.password = "segura123";     // Setter → ahora sí cambia
console.log(u.autenticar("segura123")); // true
```

---

## 🔹 Explicación detallada del ejemplo

1. `#password` → es una **propiedad privada** (solo accesible dentro de la clase).
    
2. `get password()` → permite obtener la contraseña, pero en lugar de devolver el valor real, siempre devuelve `"*****"`.
    
    - Esto evita exponer datos sensibles.
        
3. `set password(nuevaClave)` → se ejecuta cada vez que intentamos **asignar un nuevo valor** a `password`.
    
    - Aquí validamos que la contraseña tenga al menos 6 caracteres.
        
    - Si no cumple, no la modifica y muestra un mensaje de error.
        
4. `autenticar(clave)` → método que compara la clave interna con la ingresada.
    

De esta forma, logramos **encapsulamiento real**: protegemos los datos y controlamos cómo se acceden y modifican.

---

## 🔹 Ejemplo 2: Getter como propiedad calculada

Un getter no siempre devuelve un atributo oculto. También puede **calcular un valor dinámico**.

```javascript
class Rectangulo {
  constructor(ancho, alto) {
    this.ancho = ancho;
    this.alto = alto;
  }

  // Getter para calcular el área
  get area() {
    return this.ancho * this.alto;
  }
}

let r = new Rectangulo(10, 5);
console.log(r.area); // 50 (se calcula automáticamente)
```

🔎 Aquí no existe una propiedad llamada `area` almacenada en memoria.  
Se **calcula en el momento** cada vez que accedemos a `r.area`.

---

## 🔹 Ejemplo 3: Uso combinado en propiedades calculadas y validadas

```javascript
class Persona {
  constructor(nombre, nacimiento) {
    this.nombre = nombre;
    this.nacimiento = nacimiento; // Año de nacimiento
  }

  // Getter: calcula la edad actual
  get edad() {
    let añoActual = new Date().getFullYear();
    return añoActual - this.nacimiento;
  }

  // Setter: evita fechas inválidas
  set nacimiento(año) {
    if (año > new Date().getFullYear()) {
      console.log("El año de nacimiento no puede ser futuro");
    } else {
      this._nacimiento = año;
    }
  }

  get nacimiento() {
    return this._nacimiento;
  }
}

let p = new Persona("Ana", 2000);
console.log(p.edad); // muestra la edad calculada
p.nacimiento = 2050; // "El año de nacimiento no puede ser futuro"
```

---

## 🔹 Ventajas de usar Getters y Setters

- Permiten **controlar la lógica de acceso** a las propiedades.
    
- Evitan **modificaciones directas inseguras**.
    
- Ayudan a mantener la **integridad del objeto**.
    
- Facilitan la implementación de **propiedades calculadas** sin necesidad de métodos explícitos.
    
- Aumentan la **legibilidad del código**, ya que accedemos como si fueran propiedades normales, pero con lógica extra detrás.
    

---

✅ En resumen:

- **Getter** → método que devuelve un valor calculado o encapsulado como si fuera una propiedad.
    
- **Setter** → método que valida o controla la asignación de un valor.
    
- Son clave en **encapsulamiento** y en la creación de **APIs más seguras y claras** dentro de la POO en JavaScript.
    

---