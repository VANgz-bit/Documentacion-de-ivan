### 📘 **Apunte: `instanceof` en JavaScript**

#### 🔹 **Definición general**

El operador `instanceof` en JavaScript se utiliza para comprobar si un objeto **es una instancia de una clase o función constructora específica**, o si **hereda** de ella en su cadena de prototipos.

En otras palabras, sirve para verificar si un objeto fue creado (directa o indirectamente) a partir de una determinada clase o función constructora.

---

#### 🔹 **Sintaxis**

```js
objeto instanceof Constructor
```

- **`objeto`** → Es el valor u objeto que queremos comprobar.
    
- **`Constructor`** → Es la función constructora o clase con la cual queremos comparar.
    

El resultado de la operación será:

- `true` → si el objeto **proviene** de la clase o constructor especificado (ya sea directa o indirectamente).
    
- `false` → si **no** proviene de esa clase o no tiene ese constructor en su cadena de prototipos.
    

---

#### 🔹 **Ejemplo básico con clases**

```js
class Animal {}
class Perro extends Animal {}

const miPerro = new Perro();

console.log(miPerro instanceof Perro);   // true
console.log(miPerro instanceof Animal);  // true
console.log(miPerro instanceof Object);  // true
console.log(miPerro instanceof Array);   // false
```

**Explicación:**

- `miPerro` fue creado a partir de `Perro`, por lo tanto `miPerro instanceof Perro` devuelve `true`.
    
- Como `Perro` hereda de `Animal`, también devuelve `true` para `Animal`.
    
- Todos los objetos en JavaScript heredan de `Object`, por eso también devuelve `true`.
    
- Pero `miPerro` **no hereda** de `Array`, por eso da `false`.
    

---

#### 🔹 **Ejemplo con funciones constructoras**

```js
function Persona(nombre) {
  this.nombre = nombre;
}

const juan = new Persona("Juan");

console.log(juan instanceof Persona); // true
console.log(juan instanceof Object);  // true
```

**Explicación:**

- `juan` fue creado mediante `new Persona()`, por lo tanto es una instancia de `Persona`.
    
- A su vez, toda función constructora hereda de `Object`, por eso también devuelve `true`.
    

---

#### 🔹 **Comportamiento con herencia y prototipos**

Cuando `instanceof` se ejecuta, **no compara el tipo directamente**, sino que **recorre la cadena de prototipos** (`[[Prototype]]`) del objeto buscando si coincide con el prototipo del constructor.

Por ejemplo:

```js
miPerro instanceof Animal
```

Internamente, JavaScript verifica si el prototipo de `Animal` (`Animal.prototype`) aparece en la cadena de prototipos de `miPerro`.  
Si lo encuentra, devuelve `true`.

---

#### 🔹 **Ejemplo visual del recorrido**

```js
miPerro → Perro.prototype → Animal.prototype → Object.prototype → null
```

`instanceof` recorre esta cadena en busca del prototipo correspondiente al constructor que se le pasa como referencia.

---

#### 🔹 **Uso con tipos nativos**

`instanceof` también puede aplicarse a objetos nativos:

```js
console.log([] instanceof Array);     // true
console.log([] instanceof Object);    // true
console.log({} instanceof Object);    // true
console.log(() => {} instanceof Function); // true
```

Sin embargo, hay que tener cuidado con valores primitivos, ya que no son objetos:

```js
console.log("hola" instanceof String); // false
console.log(new String("hola") instanceof String); // true
```

La primera comparación da `false` porque `"hola"` es un **primitivo**, no un objeto `String`.  
La segunda da `true` porque se crea un objeto con `new String()`.

---

#### 🔹 **Limitaciones**

1. `instanceof` **solo funciona con objetos**, no con tipos primitivos.
    
2. Si se comparan objetos creados en **diferentes contextos globales** (por ejemplo, en diferentes ventanas o iframes del navegador), `instanceof` puede devolver resultados incorrectos, ya que cada contexto tiene sus propias referencias a constructores como `Array`, `Object`, etc.
    
3. No es adecuado para determinar el **tipo exacto** de datos cuando solo queremos saber si algo es, por ejemplo, un número o una cadena. En esos casos se usa `typeof`.
    

---

#### 🔹 **Comparación con `typeof`**

|Operador|Devuelve para objetos|Devuelve para primitivos|Caso de uso principal|
|---|---|---|---|
|`instanceof`|`true` / `false` según la cadena de prototipos|No aplica (falla)|Saber si un objeto proviene de una clase o constructor|
|`typeof`|`"object"` o `"function"`|`"string"`, `"number"`, etc.|Saber el tipo de un valor primitivo o función|

---

#### 🔹 **Ejemplo final combinado**

```js
class Vehiculo {}
class Auto extends Vehiculo {}

const ferrari = new Auto();

console.log(ferrari instanceof Auto);       // true
console.log(ferrari instanceof Vehiculo);   // true
console.log(ferrari instanceof Object);     // true
console.log(typeof ferrari);                // "object"
```

---

#### 🔹 **Conclusión**

El operador `instanceof` es una herramienta poderosa para **verificar relaciones de herencia y origen de objetos** en JavaScript.  
Funciona recorriendo la cadena de prototipos hasta encontrar (o no) la referencia al prototipo del constructor indicado.  
Es ideal cuando se trabaja con **clases, funciones constructoras y herencia**, pero no sustituye a `typeof` cuando se necesita identificar **tipos primitivos**.

---
