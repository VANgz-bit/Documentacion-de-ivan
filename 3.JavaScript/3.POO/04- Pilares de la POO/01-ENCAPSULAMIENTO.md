# 04 - Encapsulamiento

---

## 🔹 Definición

El **encapsulamiento** es el principio de la Programación Orientada a Objetos que busca **proteger el estado interno de un objeto** (sus propiedades), de manera que solo pueda ser accedido o modificado a través de **métodos controlados**.

En otras palabras:

- **Sin encapsulación** → cualquiera puede cambiar cualquier dato del objeto en cualquier momento.
    
- **Con encapsulación** → se controla qué se puede leer, qué se puede modificar y cómo.
    

👉 La idea central es que el **objeto decide qué mostrar y qué ocultar**, manteniendo la coherencia de su estado.

---

## 🔹 Problema sin encapsulación

Imaginemos una **cuenta bancaria**:

```js
class CuentaBancaria {
  constructor(saldo) {
    this.saldo = saldo;
  }
}

let cuenta = new CuentaBancaria(1000);
cuenta.saldo = -999999;  // 🚨 ¡Se rompe toda la lógica!
console.log(cuenta.saldo); // -999999
```

Aquí cualquiera puede modificar el saldo a mano y dejar la cuenta en un estado inválido.  
Esto demuestra la necesidad de **encapsular**.

---

## 🔹 Soluciones históricas en JavaScript

### 1. Convención con guion bajo

Antes de que existieran propiedades privadas, se usaba la convención de nombrar atributos internos con un **guion bajo** `_`.  
No es seguridad real, solo un acuerdo entre programadores.

```js
class CuentaBancaria {
  constructor(saldo) {
    this._saldo = saldo;
  }

  getSaldo() {
    return this._saldo;
  }

  depositar(monto) {
    this._saldo += monto;
  }

  retirar(monto) {
    if (monto <= this._saldo) {
      this._saldo -= monto;
    } else {
      console.log("Fondos insuficientes.");
    }
  }
}

let cuenta = new CuentaBancaria(1000);
console.log(cuenta.getSaldo()); // 1000
cuenta.depositar(500);
console.log(cuenta.getSaldo()); // 1500
cuenta._saldo = -9999; // 🚨 Se puede romper igual, porque no es privado
```

---

### 2. Encapsulación con _closures_

Otra técnica previa era usar **funciones constructoras** con variables privadas creadas dentro de un closure.

```js
function CuentaBancaria(saldo) {
  let _saldo = saldo; // privado por closure

  this.getSaldo = function() {
    return _saldo;
  };

  this.depositar = function(monto) {
    _saldo += monto;
  };

  this.retirar = function(monto) {
    if (monto <= _saldo) {
      _saldo -= monto;
    } else {
      console.log("Fondos insuficientes.");
    }
  };
}

let cuenta = new CuentaBancaria(1000);
console.log(cuenta.getSaldo()); // 1000
cuenta.depositar(500);
console.log(cuenta.getSaldo()); // 1500
console.log(cuenta._saldo); // undefined (no es accesible desde afuera ✅)
```

👉 Aquí sí logramos ocultar el dato, pero la sintaxis es menos clara y se pierde la ventaja de `class`.

---

## 🔹 Encapsulación moderna (ES2020+)

JavaScript incorporó **propiedades privadas** usando `#`.  
Esto sí es seguridad real: no se pueden acceder desde fuera de la clase.

```js
class CuentaBancaria {
  #saldo; // propiedad privada

  constructor(saldoInicial) {
    this.#saldo = saldoInicial;
  }

  get saldo() {  // getter
    return this.#saldo;
  }

  depositar(monto) {
    this.#saldo += monto;
  }

  retirar(monto) {
    if (monto <= this.#saldo) {
      this.#saldo -= monto;
    } else {
      console.log("Fondos insuficientes.");
    }
  }
}

let cuenta = new CuentaBancaria(1000);
console.log(cuenta.saldo); // 1000
cuenta.depositar(300);
console.log(cuenta.saldo); // 1300

// 🚨 Error real: no se puede acceder desde fuera
console.log(cuenta.#saldo); // ❌ SyntaxError
```

---

## 🔹 Relación con getters y setters

El **encapsulamiento** se complementa con los **getters y setters**, que permiten:

- Leer propiedades privadas de forma controlada.
    
- Validar o modificar datos antes de guardarlos.
    

Ejemplo extendido:

```js
class Usuario {
  #password;

  constructor(nombre, password) {
    this.nombre = nombre;
    this.#password = password;
  }

  get password() {
    return "*****"; // nunca muestra el real
  }

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

let u = new Usuario("Iván", "123456");
console.log(u.password); // "*****"
u.password = "abc";      // "La clave es demasiado corta"
u.password = "segura123";
console.log(u.autenticar("segura123")); // true
```
---
## EXPLICACION DEL EJEMPLO


### 🔹 1. Definición de la clase

```js
class Usuario {
  #password; // propiedad privada
```

- Aquí creamos una clase `Usuario`.
    
- La propiedad `#password` está declarada como **privada**, lo que significa que **solo puede usarse dentro de la clase**.  
    👉 Si intentamos `usuario.#password` desde afuera, da error.
    

---

### 🔹 2. El constructor

```js
  constructor(nombre, password) {
    this.nombre = nombre;
    this.#password = password;
  }
```

- El constructor recibe `nombre` y `password`.
    
- `this.nombre` queda como público (se puede acceder desde afuera).
    
- `this.#password` queda como **privado**.
    

Ejemplo:

```js
let u = new Usuario("Iván", "123456");
console.log(u.nombre);   // Iván  (público)
console.log(u.#password); // ❌ Error (porque es privado)
```

---

### 🔹 3. Getter `get password`

```js
  get password() {
    return "*****"; // nunca muestra el real
  }
```

- Un **getter** permite leer una propiedad como si fuera un atributo, pero en realidad ejecuta un método.
    
- Aquí, cuando alguien hace `u.password`, en vez de mostrar la clave real, devuelve `"*****"`.
    
- Esto se hace por **seguridad**: nunca exponemos la contraseña directamente.
    

Ejemplo:

```js
console.log(u.password); // "*****"
```

---

### 🔹 4. Setter `set password`

```js
  set password(nuevaClave) {
    if (nuevaClave.length >= 6) {
      this.#password = nuevaClave;
    } else {
      console.log("La clave es demasiado corta");
    }
  }
```

- Un **setter** sirve para modificar una propiedad como si fuese un atributo.
    
- Pero aquí agregamos una **validación**:
    
    - Si la nueva clave tiene 6 o más caracteres, se guarda.
        
    - Si es más corta, no la guarda y muestra un mensaje de error.
        

Ejemplo:

```js
u.password = "abc";       // "La clave es demasiado corta"
u.password = "segura123"; // ✅ se guarda porque cumple la condición
```

---

### 🔹 5. Método `autenticar`

```js
  autenticar(clave) {
    return this.#password === clave;
  }
```

- Este método compara la clave ingresada con la que está guardada en la propiedad privada.
    
- Devuelve `true` si son iguales, `false` en caso contrario.
    

Ejemplo:

```js
console.log(u.autenticar("segura123")); // true
console.log(u.autenticar("otraClave")); // false
```

---

### 🔹 6. Ejecución paso a paso del ejemplo completo

```js
let u = new Usuario("Iván", "123456"); 
```

👉 Creamos un usuario con nombre `"Iván"` y contraseña `"123456"`.

```js
console.log(u.password); 
```

👉 Usa el **getter** → muestra `"*****"` en lugar de la clave real.

```js
u.password = "abc";
```

👉 Usa el **setter** → como tiene menos de 6 caracteres, no cambia la clave.  
Resultado: `"La clave es demasiado corta"`.

```js
u.password = "segura123";
```

👉 Usa el **setter** → como tiene 9 caracteres, ahora sí actualiza la clave privada.

```js
console.log(u.autenticar("segura123")); 
```

👉 Llama al método → compara `"segura123"` con la contraseña privada guardada.  
Resultado: `true`.

---

✅ **Resumen final del ejemplo**

- `#password` es privado, nadie puede verlo directamente.
    
- El getter solo devuelve `"*****"`.
    
- El setter controla si la nueva clave es válida antes de guardarla.
    
- `autenticar()` permite comprobar si la clave ingresada coincide con la guardada.
    

---


## 📌 Conclusión

- El encapsulamiento es **controlar el acceso al estado interno de un objeto**.
    
- En JavaScript evolucionó:
    
    1. Convenciones (`_propiedad`).
        
    2. Closures para datos privados.
        
    3. Propiedades privadas con `#` (moderno y recomendado).
        
- Se apoya en **getters y setters** para exponer de manera segura lo que conviene mostrar.
    

👉 Es el primer pilar de POO porque garantiza **seguridad y coherencia** en los objetos.

---
