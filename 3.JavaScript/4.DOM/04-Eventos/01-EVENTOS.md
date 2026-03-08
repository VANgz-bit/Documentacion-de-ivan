# **🔷 EVENTOS EN EL DOM 
## **1. ¿Qué es un evento? (Definición profunda)**

Un **evento** es cualquier suceso detectado por el navegador que puede activar una respuesta programada mediante JavaScript.

Esto significa que:

- El navegador **está constantemente escuchando** lo que ocurre en el documento.
    
- Cuando algo sucede (un click, una pulsación de tecla, una carga de página, etc.), se **genera un objeto de evento**, el cual contiene información detallada sobre lo que ocurrió.
    
- Ese objeto se envía automáticamente a la función encargada de manejarlo (el **callback**), y allí podemos reaccionar programáticamente.
    

Ejemplo conceptual:

> “El usuario hizo click en el botón”.  
> El navegador detecta ese click → crea un objeto `MouseEvent` → se lo entrega al JavaScript → nuestro código se ejecuta.

---

## **2. ¿Qué es un callback en el contexto de eventos?**

Un **callback** es una **función que NO se ejecuta en el momento en que la escribimos**, sino que se pasa como referencia a otro mecanismo (por ejemplo, un listener) para que se ejecute **después**, cuando ocurra algo específico.

### **Definición formal de callback:**

> Es una función que se pasa como argumento a otra función, con el objetivo de que sea ejecutada posteriormente como consecuencia de un evento o acción.

### **Ejemplo básico**

```js
function saludar() {
  console.log("Hola");
}

btn.addEventListener("click", saludar);
```

Aquí:

- `saludar` es un callback.
    
- NO se está ejecutando → **no lleva `()`**.
    
- Se ejecutará **después**, cuando ocurra el evento `"click"`.
    

Si escribieras:

```js
btn.addEventListener("click", saludar());
```

→ **Ejecutarías la función inmediatamente**, lo cual es incorrecto.

---

## **3. EVENT HANDLERS (forma antigua)**

### **3.1 Qué son**

Los “event handlers” son la forma original de manejar eventos en JavaScript.  
Su característica principal es que el manejador del evento se coloca **dentro del HTML** como atributo.

Se construyen con la palabra clave **`on`** seguida del nombre del evento:

- `onclick`
    
- `onchange`
    
- `onload`
    
- `onmouseover`
    

### **3.2 Ejemplo clásico**

```html
<button onclick="alert('Hola')">Click</button>
```

En este caso:

- El handler está dentro del HTML.
    
- El código es una cadena de texto evaluada cuando ocurre el evento.
    
- No hay separación entre “estructura” (HTML) y “comportamiento” (JS), cosa que hoy se considera mala práctica.
    

### **3.3 Limitaciones técnicas**

#### 1️⃣ Solo permiten **una función por evento**

```js
button.onclick = fn1
button.onclick = fn2  // fn1 se pierde
```

#### 2️⃣ Impiden separar lógica y estructura

Violando el principio de **separación de responsabilidades** (HTML ≠ JS).

#### 3️⃣ No se pueden remover fácilmente.

#### 4️⃣ No interactúan correctamente con el flujo de eventos (bubbling/capturing).

Por eso **ya NO SE RECOMIENDAN** en código profesional moderno.

---

## **4. EVENT LISTENERS (forma moderna)**

### **4.1 Qué son**

Los **Event Listeners** son la forma estándar actual para manejar eventos.  
Se definen con el método:

```js
element.addEventListener(evento, callback, opciones);
```

### **4.2 Ventajas técnicas**

✔ Permiten **múltiples callbacks** para un mismo evento.  
✔ Separan HTML y JS.  
✔ Permiten eliminar listeners.  
✔ Se integran totalmente con el sistema de propagación (bubbling/capturing).  
✔ Son compatibles con programación modular, clases, componentes, etc.

### **4.3 Ejemplo básico**

```js
button.addEventListener("click", () => {
  console.log("Hiciste click");
});
```

### **4.4 Remover un listener**

```js
function alerta(){ console.log("Hola") }
button.addEventListener("click", alerta);
button.removeEventListener("click", alerta);
```

No es posible remover handlers colocados en HTML.

---

## **5. DIFERENCIA FUNDAMENTAL ENTRE HANDLER Y LISTENER**

|Característica|Handler (`onclick=""`)|Listener (`addEventListener`)|
|---|---|---|
|Ubicación|HTML o propiedad JS|Solo JS|
|Cantidad|1 por evento|Múltiples|
|Remover|No|Sí|
|Modernidad|Obsoleto|Estándar|
|Control de flujo|No|Sí|
|Buenas prácticas|No|Sí|

---
## **6. EL EVENT FLOW (FLUJO DEL EVENTO)**

### _Una explicación clara, conceptual y profunda_

En JavaScript, cuando ocurre un evento en algún elemento del **DOM**, ese evento **no se limita al elemento donde ocurre**. En realidad, se genera un **recorrido completo** por el árbol del DOM que consta de **tres fases distintas**:

---

## 🔵 **FASE 1: Capturing (Fase de Captura)**

El evento comienza su recorrido **desde lo más alto del árbol del DOM** y baja hasta el objetivo final:

```
window
  ⬇
document
  ⬇
<body>
  ⬇
<div padre>
  ⬇
<button objetivo>
```

🔸 En esta fase, **el evento solo recorre sin activar callbacks por defecto**.  
🔸 **Solo los listeners especialmente registrados para esta fase** pueden ejecutar código en este momento.

> ✨ Esta fase es útil cuando se quiere interceptar la interacción antes de que llegue al objetivo.

---

## 🔵 **FASE 2: Target (Fase Objetivo)**

En este punto, el evento **ha llegado al elemento donde fue disparado físicamente**.

Ejemplo: si hacemos click sobre un `<button>`, ese botón es el **target**.

🔸 Aquí es donde se ejecutan los callbacks **directamente asociados al objetivo**, independientemente de si están configurados para captura o burbujeo.

---

## 🔵 **FASE 3: Bubbling (Fase de Burbujeo)**

Una vez que el evento llega al objetivo y ejecuta los handlers asociados, comienza a **subir el árbol del DOM** hacia los nodos padre, repitiendo el camino pero en sentido contrario.

```
<button objetivo>
  ⬆
<div padre>
  ⬆
<body>
  ⬆
document
  ⬆
window
```

🔸 **Esta fase está activa por defecto** en todos los eventos (excepto algunos muy específicos como `focus` o `blur`).

🔸 Es muy común que el evento se “propague” a los elementos padres y que sus handlers también se ejecuten.

> 💡 Ejemplo típico: haces click en un botón dentro de un contenedor. Si ambos tienen listeners de click, ambos recibirán el evento, primero el botón y luego el contenedor.

---

## 🧠 ¿Por qué importa el flujo?

Conociendo estos mecanismos, es posible:

- **Controlar dónde y cuándo se ejecuta código**, según la fase.
    
- **Delegar eventos** (por ejemplo, escuchar clicks en un contenedor padre por eficiencia).
    
- **Detener el flujo** si se necesita.
    
- Evitar conflictos entre event listeners en elementos hijos y padres.
    

---

## 🛑 Detener el flujo del evento

JavaScript te permite detener la propagación del evento durante su recorrido.

### 🔸 `event.stopPropagation()`

Detiene la **propagación hacia otros elementos**, evitando que se ejecute cualquier handler en fases posteriores.

```js
hijo.addEventListener("click", (e) => {
  console.log("Solo hijo");
  e.stopPropagation();
});
```

Resultado:

```
Solo hijo
```

✋ El evento **no subirá al padre**, incluso si hay handlers registrados allí.

---

### 🔸 `event.stopImmediatePropagation()`

Detiene **TODOS los listeners** del mismo evento en el mismo elemento, incluidos otros listeners en el mismo nivel.

---

## 🔧 Activando la fase de **captura** (capturing)

Al usar `addEventListener`, podemos indicar si queremos escuchar el evento durante la fase de captura:

```js
padre.addEventListener("click", () => console.log("PADRE"), true);
```

El tercer parámetro `true` indica capturar en la fase de **captura** y no en burbujeo.

---

## 🧪 Ejemplo completo

```html
<div id="padre">
  <button id="hijo">Click</button>
</div>
```

```js
padre.addEventListener("click", () => console.log("PADRE"), true); // fase capturadora
hijo.addEventListener("click", () => console.log("HIJO"));        // fase burbujeo
padre.addEventListener("click", () => console.log("PADRE BURBUJEO"));
```

🔹 Resultado al hacer click en el botón:

```
PADRE        ← Capturing
HIJO         ← Target
PADRE BURBUJEO ← Bubbling
```

---

## 📚 Resumen Esquemático

|Fase|Dirección|Ejecuta handlers por defecto|Propósito|
|---|---|---|---|
|Capturing|🔽 Descendiendo|❌ No|Interceptar antes de llegar|
|Target|🎯 Elemento del evento|✔️ Sí|Ejecutar acción principal|
|Bubbling|🔼 Ascendiendo|✔️ Sí|Delegación y control general|

---
## **7. ¿Pueden los eventos recibir parámetros?**

🔷 **El evento SIEMPRE recibe UN SOLO parámetro automáticamente**  
Ese parámetro es el objeto **`Event`**, y contiene información sobre lo ocurrido.

```js
element.addEventListener("click", function(event){
  console.log(event);
});
```

Ese `event` puede tener muchas propiedades:

|Propiedad|Significado|
|---|---|
|`target`|Elemento que disparó el evento|
|`type`|Tipo de evento (click, input…)|
|`clientX`|Posición X del mouse|
|`key`|Tecla presionada (en keydown)|
|`timeStamp`|Tiempo desde que la página cargó|

---

### ❗ Importante

**NO podemos agregarle parámetros custom al evento desde JavaScript**

✔ Pero sí podemos crear **funciones intermedias**:

```js
button.addEventListener("click", ()=> ejecutar(4, 5));
```

Esto **no modifica el evento**, sino que usa una función anónima como puente.

---

### Ejemplo completo

```js
function sumar(a, b, evento){
  console.log(a + b);
  console.log(evento.type);
}

button.addEventListener("click", e => sumar(3, 7, e));
```

✔ La función `sumar` ahora recibe **parámetros propios + el objeto evento**.

---

## **8. ¿Por qué el parámetro se llama “e”?**

Podrías llamarlo:

- `e`
    
- `event`
    
- `evt`
    
- `pepito`
    

Pero por convención profesional se escribe **`e`** o **`event`**.

Ejemplo real de uso:

```js
input.addEventListener("input", event=>{
  console.log(event.target.value);
});
```

---

# **⛔ MITO A ELIMINAR**

❌ "Los eventos solo pueden recibir un parámetro"  
✔ Los listeners **solo reciben 1 parámetro automático (event)**  
✔ Pero **podés pasar parámetros adicionales mediante funciones wrapper**.

---
