# **AJAX — Desarrollo completo y conceptual**

## **Introducción a AJAX**

AJAX es un **patrón de comunicación web asíncrona** que permite que una aplicación web se comunique con un servidor **sin necesidad de recargar la página completa**. Desde el punto de vista del navegador, esto significa que JavaScript puede enviar una petición HTTP, continuar ejecutando otras tareas y reaccionar cuando la respuesta llega.

Este enfoque rompe con el modelo tradicional de navegación, donde cada interacción importante implicaba una recarga total del documento HTML. Con AJAX, el navegador pasa a comportarse como un **cliente activo**, capaz de solicitar datos específicos y actualizar solo partes concretas de la interfaz.

Aunque el nombre incluye _XML_, en el desarrollo moderno **AJAX trabaja casi exclusivamente con JSON**, que es el formato de datos más utilizado para representar información estructurada en la comunicación cliente-servidor.

---

## **La petición HTTP GET**

Antes de hablar del objeto técnico, es fundamental definir **qué es una petición GET**, ya que es el tipo de petición que estamos usando.

Una **petición GET** es un método HTTP cuyo propósito es **solicitar información a un servidor**, sin modificar el estado del recurso solicitado. En otras palabras, GET se utiliza cuando el cliente quiere **leer datos**, no crearlos ni modificarlos.

Desde el punto de vista conceptual:

- El cliente pide un recurso identificado por una URL
    
- El servidor responde con los datos asociados a ese recurso
    
- No se envía un cuerpo de datos en la petición
    
- La respuesta suele venir acompañada de un código de estado y, en aplicaciones modernas, de datos en formato JSON
    

Por este motivo, GET es el método más utilizado para **consultas**, **listas**, **búsquedas** y **carga inicial de información**.

---

## **El objeto `XMLHttpRequest`**

El objeto `XMLHttpRequest` es una **API nativa del navegador** que permite crear y manejar peticiones HTTP desde JavaScript. No representa únicamente “una llamada al servidor”, sino **todo el ciclo de vida de una petición**, incluyendo su configuración, envío, estados intermedios, eventos y respuesta final.

Cuando se instancia un `XMLHttpRequest`, se obtiene un objeto que:

- Mantiene información sobre el estado de la comunicación
    
- Expone propiedades con los datos de la respuesta
    
- Emite eventos a medida que la petición avanza
    

```js
const xhr = new XMLHttpRequest();
```

A partir de este momento, `xhr` representa una **petición HTTP aún no enviada**, pero lista para ser configurada.

# **Propiedades principales de `XMLHttpRequest`**

El objeto `XMLHttpRequest` mantiene internamente **toda la información relevante de una petición HTTP** mientras esta se configura, se envía y se resuelve.  
Las propiedades principales son aquellas que **se consultan constantemente en la práctica**, porque permiten saber **en qué estado está la petición**, **si fue exitosa** y **qué datos devolvió el servidor**.

---

## **`readyState`**

Mencionada mas adelante.

---

## **`status`**

`status` contiene el **código de estado HTTP** devuelto por el servidor.  
Esta propiedad expresa el **resultado real de la petición**, según las reglas del protocolo HTTP.

A diferencia de `readyState`, que habla de progreso, `status` habla de **éxito o error**.

Algunos ejemplos importantes:

- `200` → la petición fue exitosa
    
- `404` → el recurso no existe
    
- `500` → error interno del servidor
    

`status` solo debe evaluarse cuando la petición ya terminó (`readyState === 4` o evento `load`), ya que antes de eso su valor no es confiable.

En aplicaciones reales, **toda la lógica de control depende de esta propiedad**.

---

## **`responseText`**

`responseText` contiene el **cuerpo de la respuesta del servidor en formato texto**.

Aunque el servidor envíe datos estructurados (por ejemplo JSON), el navegador **los recibe inicialmente como texto plano**. Por ese motivo, `responseText` suele ser un string que luego debe ser procesado.

Cuando se trabaja con JSON, esta propiedad se combina directamente con la deserialización:

```js
const datos = JSON.parse(xhr.responseText);
```

Esta propiedad es central en AJAX clásico, porque representa el **puente entre el servidor y el código JavaScript**.

---

## **`response`**

`response` representa la **respuesta procesada**, no necesariamente en texto.

Su valor depende del tipo de respuesta configurado mediante `responseType`.  
Cuando no se configura nada, `response` suele coincidir con `responseText`, pero su importancia aparece cuando se trabaja con formatos más avanzados.

En el caso de JSON, si se configura correctamente, `response` puede devolver directamente un **objeto JavaScript**, eliminando la necesidad de usar `JSON.parse()`.

Conceptualmente, `response` es la propiedad que mejor refleja **el dato final que la aplicación va a usar**.

---

## **`responseType`**

`responseType` permite indicar **cómo debe interpretar el navegador la respuesta del servidor**.

Se establece antes de llamar a `send()` y define el tipo de dato que se almacenará en `response`.

Cuando se trabaja con APIs modernas que devuelven JSON, configurar esta propiedad permite simplificar mucho el código y evitar errores de parsing manual.

Desde el punto de vista conceptual, `responseType` define **el contrato de datos** entre el cliente y el servidor.

---

## **Idea clave para entender estas propiedades**

- `readyState` indica **cuándo** se puede trabajar
    
- `status` indica **si salió bien o mal**
    
- `responseText` indica **qué llegó en texto**
    
- `response` indica **el dato ya procesado**
    
- `responseType` define **cómo se procesa ese dato**
    

Estas cinco propiedades forman el **núcleo práctico de `XMLHttpRequest`** y explican por qué AJAX funciona como puente entre HTTP y JavaScript.

---

## **El proceso de `open()`**

El método `open()` es el paso donde se **define formalmente la petición**. En este punto se establece **qué se va a pedir**, **cómo** y **de qué manera se va a ejecutar**, pero todavía **no se envía nada al servidor**.

```js
xhr.open("GET", "https://api.ejemplo.com/usuarios", true);
```

Conceptualmente, `open()` cumple varias funciones importantes al mismo tiempo:

1. **Define el método HTTP**, en este caso `GET`, indicando que la intención es obtener datos.
    
2. **Asocia la petición a una URL**, que identifica el recurso solicitado.
    
3. **Establece el modo asíncrono**, lo que permite que el navegador no se bloquee mientras espera la respuesta.
    

Después de ejecutar `open()`, la petición entra en un estado interno en el que ya puede:

- Configurar encabezados
    
- Asociar eventos
    
- Prepararse para el envío
    

Pero todavía **no existe comunicación con el servidor**.

---

## **El proceso de `send()`**

El método `send()` es el punto exacto en el que la petición **sale del navegador hacia el servidor**.

```js
xhr.send();
```

Desde el punto de vista conceptual:

- El navegador construye el mensaje HTTP
    
- Se establece la conexión con el servidor
    
- Comienza la recepción progresiva de la respuesta
    

En una petición GET, `send()` no recibe argumentos porque **los datos no se envían en el cuerpo**, sino que la solicitud se basa únicamente en la URL y sus parámetros.

A partir de este momento, el objeto `XMLHttpRequest` comienza a cambiar su estado interno y a emitir eventos.

---

## **Estados internos de una petición (`readyState`)**

Durante su vida, una petición AJAX pasa por **distintos estados internos** que representan el progreso de la comunicación entre el cliente y el servidor. Estos estados se reflejan en la propiedad `readyState`.

Cada cambio de estado indica que la petición avanzó a una nueva fase del proceso.

Los estados son:

- **0 (UNSENT)**  
    La petición fue creada, pero aún no se llamó a `open()`.
    
- **1 (OPENED)**  
    Se llamó a `open()`. La petición está configurada, pero todavía no fue enviada.
    
- **2 (HEADERS_RECEIVED)**  
    El servidor respondió y se recibieron los encabezados HTTP. Todavía no está disponible el cuerpo de la respuesta.
    
- **3 (LOADING)**  
    El navegador está recibiendo el cuerpo de la respuesta de forma progresiva.
    
- **4 (DONE)**  
    La petición terminó completamente. La respuesta ya fue recibida, independientemente de si fue exitosa o no.
    

El estado **más importante es `4 (DONE)`**, ya que indica que ya se puede evaluar la respuesta y el código de estado HTTP.

---

## **Evento `readystatechange`**

Cada vez que `readyState` cambia, el objeto `XMLHttpRequest` dispara el evento `readystatechange`. Este evento permite observar **todas las transiciones internas de la petición**.

Ejemplo con eventos:

```js
const xhr = new XMLHttpRequest();

xhr.open("GET", "https://api.ejemplo.com/usuarios", true);

xhr.addEventListener("readystatechange", () => {
  if (xhr.readyState === 4) {
    if (xhr.status === 200) {
      const datos = JSON.parse(xhr.responseText);
      console.log(datos);
    } else {
      console.error("Error HTTP:", xhr.status);
    }
  }
});

xhr.send();
```

Este enfoque es válido, pero tiene una particularidad importante:  
el evento se ejecuta **varias veces**, no solo al finalizar la petición. Por eso requiere verificar explícitamente el estado final.

---

## **Códigos de estado HTTP**

Cuando la petición alcanza el estado `DONE`, el servidor responde con un **código de estado HTTP**, accesible mediante `xhr.status`. Este código indica el resultado real de la operación.

Los estados más importantes en la práctica son:

- **200 (OK)**: la petición fue exitosa.
    
- **201 (Created)**: el recurso fue creado correctamente.
    
- **400 (Bad Request)**: la solicitud es incorrecta.
    
- **401 (Unauthorized)**: falta autenticación.
    
- **403 (Forbidden)**: no hay permisos.
    
- **404 (Not Found)**: el recurso no existe.
    
- **500 (Internal Server Error)**: error del servidor.
    

Evaluar estos códigos es esencial para decidir cómo debe reaccionar la aplicación.

---

## **Evento `load`: forma recomendada**

El evento `load` se ejecuta **una sola vez**, cuando la petición terminó completamente. Esto lo convierte en una forma más clara y legible de trabajar con AJAX.

```js
const xhr = new XMLHttpRequest();

xhr.open("GET", "https://api.ejemplo.com/usuarios", true);

xhr.addEventListener("load", () => {
  if (xhr.status === 200) {
    const datos = JSON.parse(xhr.responseText);
    console.log(datos);
  } else if (xhr.status === 404) {
    console.error("Recurso no encontrado");
  } else {
    console.error("Error HTTP:", xhr.status);
  }
});

xhr.addEventListener("error", () => {
  console.error("Error de red");
});

xhr.send();
```

Acá se integran claramente:

- Eventos
    
- Códigos de estado
    
- Deserialización JSON
    

---

## **`ActiveXObject`: contexto histórico**

Antes de que `XMLHttpRequest` fuera un estándar, Internet Explorer utilizaba `ActiveXObject` para realizar comunicaciones similares. Este mecanismo fue una solución temporal y hoy está completamente obsoleto. Se estudia únicamente para entender la evolución de AJAX.

---

## **Relación final: AJAX, eventos y JSON**

AJAX define el patrón de comunicación asíncrona.  
`XMLHttpRequest` es la herramienta técnica.  
Los eventos permiten reaccionar al progreso de la petición.  
JSON es el formato de datos que se recibe y procesa.

Este conjunto de ideas es la base conceptual directa de `fetch` y Axios.

---