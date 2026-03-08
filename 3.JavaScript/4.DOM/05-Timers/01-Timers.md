# ⚡ **TIMERS EN JAVASCRIPT

Los **timers** son herramientas del navegador que permiten manejar el **tiempo** dentro de una página web.  
Son fundamentales para crear interfaces dinámicas donde:

- algo ocurre después de un momento,
    
- algo se repite con una frecuencia específica,
    
- una animación se ejecuta sincronizada con la pantalla.
    

En el fondo, un timer es como decirle al navegador:

> **"Guardá esta tarea y ejecutala más adelante, en este momento exacto."**

Los timers NO bloquean el programa.  
JavaScript sigue ejecutando código mientras el navegador espera el momento adecuado.

Existen tres grandes mecanismos:

1. acciones con retraso,
    
2. acciones repetidas,
    
3. acciones sincronizadas con la animación del navegador.
    

---

# ⭐ 1) **setTimeout()**


`setTimeout()` programa una función para que se ejecute **una sola vez** después de un tiempo específico (en milisegundos).  
No importa cuán ocupado esté el código:  
el navegador simplemente esperará ese delay y, cuando el momento llegue, colocará la función en la cola para ser ejecutada.

Esto permite:

- mostrar elementos con efecto de aparición,
    
- ejecutar un mensaje después de unos segundos,
    
- coordinar animaciones o secuencias.
    

### ✔ Ejemplo detallado

Mostrar un cartel 3 segundos después de que el usuario llega:

**HTML**

```html
<div id="bienvenida" style="opacity:0; transition:0.5s;">Bienvenido</div>
```

**JS**

```js
setTimeout(() => {
  const texto = document.getElementById("bienvenida");
  texto.style.opacity = 1;
}, 3000);
```

**Explicación clara:**

- el texto inicia invisible,
    
- `setTimeout` espera 3 segundos,
    
- luego cambia la opacidad → aparece suavemente.  
    Esto es un caso real de interfaz, no un ejemplo vacío.
    

---

# ⭐ 2) **clearTimeout()**


Cancela un timeout que todavía no se ejecutó.  
Es muy útil porque muchas veces programamos cosas que _ya no queremos que ocurran_ si el usuario hace otra acción.

Ejemplo típico: cancelar un aviso si el usuario hace click.

### ✔ Ejemplo

```js
const id = setTimeout(() => {
  panel.classList.add("mostrar");
}, 4000);

// si el usuario toca cualquier tecla, cancelamos
window.addEventListener("keydown", () => {
  clearTimeout(id);
});
```

**Por qué esto es útil:**

- El aviso no aparece si el usuario está activo.
    
- La interfaz se siente más inteligente y menos molesta.
    

---

# ⭐ 3) **setInterval()**


`setInterval()` ejecuta una función **cada cierto intervalo** de tiempo, indefinidamente.  
Es decir, programa una acción repetida en el tiempo.

Es fundamental para:

- relojes,
    
- contadores regresivos,
    
- actualización constante de datos,
    
- animaciones simples que cambian valores repetidamente.
    

### ✔ Ejemplo detallado

Un contador que sube cada segundo:

**HTML**

```html
<div id="contador"></div>
```

**JS**

```js
let numero = 0;
const contador = document.getElementById("contador");

setInterval(() => {
  numero++;
  contador.textContent = "Segundos: " + numero;
}, 1000);
```

**Explicación:**  
Cada 1 segundo actualizamos el HTML.  
Esto genera un contador visible.

---

# ⭐ 4) **clearInterval()**


Sirve para detener un intervalo repetitivo.  
Un intervalo corre para siempre a menos que lo detengamos.

Esto es importante porque:

- evita consumir recursos innecesarios,
    
- permite detener contadores cuando llegan a un valor,
    
- permite pausar procesos.
    

### ✔ Ejemplo

Contador regresivo que se detiene en 0:

```js
let tiempo = 10;
const etiqueta = document.getElementById("cuenta");

const intervalId = setInterval(() => {
  etiqueta.textContent = "Tiempo: " + tiempo;
  tiempo--;

  if (tiempo < 0) {
    clearInterval(intervalId);
    etiqueta.textContent = "Finalizado";
  }
}, 1000);
```

---

# ⭐ 5) **requestAnimationFrame()**

`requestAnimationFrame()` está diseñado **específicamente para animaciones**.  
A diferencia de los timers normales, este no usa milisegundos:  
depende del **próximo “frame” que el navegador dibuja** en la pantalla.

La ventaja es enorme:

- la animación va fluida (normalmente 60 veces por segundo),
    
- el navegador pausa la animación si la pestaña está oculta,
    
- se adapta al ritmo real del monitor.
    

En otras palabras:

> Es la forma **profesional** de mover cosas en pantalla.

### ✔ Ejemplo detallado (real)

Mover una caja hacia la derecha de forma fluida:

**HTML**

```html
<div id="caja" style="width:50px;height:50px;background:red;position:absolute;"></div>
```

**JS**

```js
let x = 0;
const caja = document.getElementById("caja");

function animar() {
  x += 3;
  caja.style.transform = `translateX(${x}px)`;

  if (x < 400) {
    requestAnimationFrame(animar);
  }
}

animar();
```

---

# ⭐ Comparación clara entre los 3 mecanismos

|Herramienta|Tipo|Uso principal|
|---|---|---|
|**setTimeout**|Una ejecución|Hacer algo después de un tiempo|
|**setInterval**|Repetición constante|Contadores, relojes, tareas periódicas|
|**requestAnimationFrame**|Animación ligada al monitor|Animaciones suaves y precisas|
