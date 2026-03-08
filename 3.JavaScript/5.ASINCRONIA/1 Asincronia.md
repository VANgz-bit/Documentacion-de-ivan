# CALLBACKS, PROMESAS Y ASYNC/AWAIT

---
# 1. CALLBACKS

## Definición central

Un **callback** es una función que se entrega como argumento a otra función para delegar en ella la responsabilidad de invocarla en un momento específico. Este “momento específico” suele ser la finalización de un proceso asincrónico o la ocurrencia de un evento.

La clave del callback es que **traslada el control de ejecución** desde quien llama a quien recibe la función.  
Ese mecanismo se denomina _inversión de control_, y es el pilar histórico del manejo asincrónico en JavaScript.

---

## Propiedades esenciales

- El callback **no se ejecuta inmediatamente**, sino cuando la función receptora decide hacerlo.
    
- Permite expresar operaciones que tardan tiempo sin bloquear el hilo principal.
    
- Requiere confiar en la función receptora, lo cual puede generar problemas cuando el flujo crece.
    
- Puede degradarse al conocido patrón **callback hell**, dificultando el mantenimiento.
    

---

## Ejemplo representativo

```js
function obtenerUsuario(callback) {
    setTimeout(() => {
        callback({ nombre: "Lucas", edad: 20 });
    }, 1000);
}

obtenerUsuario((usuario) => {
    console.log("Usuario obtenido:", usuario);
});
```

---

## Callback Hell: origen del problema

Cuando múltiples operaciones dependen una de otra:

```js
obtenerUsuario(usuario => {
    obtenerPedidos(usuario, pedidos => {
        procesarPedidos(pedidos, resultado => {
            guardarLog(resultado, () => {
                console.log("Finalizado");
            });
        });
    });
});
```

Aquí se observa un problema estructural:

- Anidación profunda
    
- Flujo difícil de seguir
    
- Manejo de errores disperso
    
- Baja legibilidad y alta fragilidad
    

Este problema motivó la creación de las Promesas.

---

# 2. PROMESAS

## Definición rigurosa

Una **Promesa** es un objeto que representa el _resultado futuro_ de una operación asincrónica. Dicho resultado no es inmediato: puede encontrarse pendiente, resolverse con éxito o fallar.

A diferencia de los callbacks, las Promesas son un mecanismo estructurado con un flujo explícito, estados bien definidos y métodos especializados para manejar el resultado.

---

## Estados y su significado

|Estado|Descripción|
|---|---|
|**pending**|La operación está realizando su proceso; no hay resultado aún.|
|**fulfilled**|La operación concluyó correctamente; hay un valor disponible.|
|**rejected**|La operación falló; se dispone de un motivo o error.|

Una vez que una Promesa pasa a `fulfilled` o `rejected`, su estado se vuelve inmutable.

---

## Componentes internos

El constructor recibe una función con dos argumentos:

```js
new Promise((resolve, reject) => {
    // resolve() para éxito
    // reject() para error
});
```

Este contrato formaliza el manejo de resultados y reemplaza la informalidad del callback puro.

---

## Métodos fundamentales

- **then()**: maneja el valor cuando la promesa se resuelve.
    
- **catch()**: maneja la razón cuando la promesa rechaza.
    
- **finally()**: se ejecuta siempre, independientemente del resultado.
    

---

## Ejemplo bien planteado

```js
function obtenerProducto() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Producto cargado correctamente");
        }, 1000);
    });
}

obtenerProducto()
    .then(res => console.log(res))
    .catch(err => console.error("Error:", err))
    .finally(() => console.log("Operación finalizada"));
```

---

# 3. LIMITACIONES QUE RESUELVE ASYNC/AWAIT

Las Promesas resolvieron el callback hell, pero cuando se encadenan múltiples `.then()`, la estructura sigue siendo esencialmente vertical:

```js
operacion1()
    .then(() => operacion2())
    .then(() => operacion3())
    .then(() => operacion4())
    .catch(console.error);
```

Aunque es correcto y legible, todavía se acerca a un estilo declarativo que no imita el flujo natural de lectura.  
Para esto surge **async/await**, que proporciona una sintaxis que mantiene la asincronía pero permite escribir código con un flujo secuencial natural.

---

# 4. ASYNC / AWAIT

## async

Una función marcada como `async` **siempre devuelve una Promesa**.  
Incluso si se retorna un valor simple, JavaScript lo envuelve automáticamente en una Promesa resuelta.

```js
async function ejemplo() {
    return 10; // Se transforma automáticamente en Promise.resolve(10)
}
```

---

## await

`await` suspende la ejecución _interna_ de la función async hasta que la Promesa proporcionada se resuelva o rechace.

Importante:

- No bloquea el programa entero.
    
- No detiene el Event Loop.
    
- Solo pausa esa función.
    

Esto permite escribir asincronía con una fluidez semejante a código secuencial.

---

## Ejemplo claro

```js
function cargar() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Cargado"), 1000);
    });
}

async function ejecutar() {
    console.log("Iniciando...");
    const resultado = await cargar();
    console.log("Resultado:", resultado);
}

ejecutar();
```

---

## Manejo de errores con try/catch

Este es uno de los puntos más fuertes del modelo async/await:  
el manejo de errores se vuelve idéntico al del código síncrono.

```js
function cargar() {
    return new Promise((resolve, reject) => {
        setTimeout(() => reject("Fallo en la carga"), 1000);
    });
}

async function ejecutar() {
    try {
        const resultado = await cargar();
        console.log(resultado);
    } catch (error) {
        console.error("Error detectado:", error);
    }
}

ejecutar();
```

---

# 5. RELACIÓN ENTRE LOS TRES MODELOS

|Modelo|Nivel|Mecanismo central|Problema que resuelve|Limitación|
|---|---|---|---|---|
|Callback|Básico|Funciones como parámetros|Primer mecanismo para asincronía|Callback Hell|
|Promesa|Intermedio|Objeto con estado y métodos|Estructura formal, encadenamiento claro|Encadenamiento largo sigue siendo verboso|
|Async/Await|Avanzado|Sintaxis sobre Promesas|Flujo legible y secuencial|Requiere comprender el modelo de Promesas|

Los tres modelos coexisten.  
Async/Await **no reemplaza** las Promesas: se construye sobre ellas.  
Las Promesas, a su vez, surgieron para estructurar mejor los callbacks.

---

# 6. UN MISMO PROCESO, TRES FORMAS

## Callback

```js
function traer(callback) {
    setTimeout(() => callback("Listo"), 1000);
}

traer(res => console.log(res));
```

---

## Promesa

```js
function traer() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Listo"), 1000);
    });
}

traer().then(res => console.log(res));
```

---

## Async/Await

```js
function traer() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Listo"), 1000);
    });
}

async function ejecutar() {
    const res = await traer();
    console.log(res);
}

ejecutar();
```

---
