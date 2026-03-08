# ⭐ **EVENTOS DE INTERFAZ (UI EVENTS)**

Los **UI Events**, o _Eventos de Interfaz de Usuario_, son una familia de eventos que se activan cuando ocurre **algún cambio importante en la ventana, el documento o ciertos elementos visuales o estructurales**.

A diferencia de los eventos del mouse o teclado, que dependen directamente de acciones físicas del usuario, los UI Events representan **eventos de alto nivel**, ligados a:

- El ciclo de carga de la página
    
- El tamaño de la ventana
    
- El desplazamiento del documento
    
- El fallo o interrupción de un recurso
    
- La selección de contenido en inputs
    
- La interacción con elementos especiales como `<details>`
    

Estos eventos suelen ser utilizados para coordinar comportamientos globales del sitio, medir estados del documento o reaccionar ante condiciones específicas de carga, error o navegación.

---

# 🟦 **1. load**


El evento `load` se activa cuando un **recurso terminó completamente su proceso de carga**, incluyendo todo lo que lo compone:

- HTML
    
- CSS
    
- imágenes
    
- scripts
    
- iframes
    
- fuentes
    
- y cualquier archivo externo vinculado
    

Es decir, marca el momento en que el navegador ya tiene **todo el contenido descargado, analizado y listo para ser usado**.

### ¿Por qué es importante?

Porque garantiza que **no se accede a recursos incompletos**. Por ejemplo:

- esperar a que una imagen esté lista para medir su tamaño
    
- ejecutar código cuando la página está 100 % cargada
    
- coordinar animaciones que dependen de la carga completa
    

### Ejemplo:

```js
window.addEventListener("load", () => {
  console.log("Todo en la página ha terminado de cargarse.");
});
```

---

# 🟦 **2. DOMContentLoaded**

_(No pertenece oficialmente a los UI Events, pero es imprescindible en el flujo de carga)_



Este evento se activa cuando **el navegador terminó de construir el DOM**, es decir, cuando ya interpretó todo el HTML y lo convirtió en nodos del DOM.

Importante:  
❗ **No espera imágenes, estilos ni recursos externos.**  
Solo el HTML.

### ¿Por qué es clave?

Porque permite ejecutar scripts antes de que las imágenes o estilos estén listos, lo cual acelera muchísimo la respuesta del sitio.

Ejemplo:

```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("El DOM está listo para trabajar.");
});
```

---

# 🟦 **3. beforeunload**



Este evento se activa cuando el usuario está **a punto de abandonar la página**:

- cerrar la pestaña
    
- actualizar
    
- navegar hacia otro enlace
    
- cerrar el navegador
    

El navegador permite mostrar un diálogo que pregunta si realmente desea salir.  
Hoy se usa para:

- advertir pérdida de datos
    
- proteger formularios no enviados
    
- evitar cierres accidentales
    

```js
window.addEventListener("beforeunload", (event) => {
  event.preventDefault();
  event.returnValue = "";
});
```

Los navegadores ya no permiten mensajes personalizados por razones de seguridad.

---

# 🟦 **4. resize**


El evento `resize` se dispara cuando la **ventana del navegador cambia de tamaño**.  
(Importante: solo funciona en `window`, no en divs comunes.)

Es esencial para manejar comportamientos **responsive** avanzados, como:

- adaptar layouts dinámicos
    
- recalcular posiciones
    
- ajustar animaciones dependientes del viewport
    
- activar o desactivar funciones según el ancho actual
    

Ejemplo:

```js
window.addEventListener("resize", () => {
  console.log("La ventana cambió de tamaño.");
});
```

---

# 🟦 **5. scroll**


El evento `scroll` se activa cuando el usuario **desplaza la página o un contenedor**.  
Es uno de los eventos más utilizados para interacción moderna.

Se usa para:

- animaciones basadas en scroll
    
- cargar contenido infinito
    
- mostrar/ocultar barras de navegación
    
- activar elementos cuando entran al viewport
    
- medir el progreso de lectura
    

```js
window.addEventListener("scroll", () => {
  console.log("Desplazamiento detectado.");
});
```

Importante:  
Es un evento que se activa **muchísimas veces por segundo**, por lo que suele necesitar técnicas de optimización como _debouncing_ o _throttling_.

---

# 🟦 **6. error**


El evento `error` se dispara cuando ocurre un **fallo en la carga o ejecución**.  
Puede aplicarse a:

- imágenes que no cargan
    
- archivos externos corruptos
    
- errores de JavaScript
    
- fuentes o scripts que fallan
    

Ejemplo en imágenes:

```js
img.addEventListener("error", () => {
  console.log("La imagen no pudo cargarse.");
});
```

Ejemplo a nivel global:

```js
window.addEventListener("error", (e) => {
  console.log("Error en el código:", e.message);
});
```

Esto permite detectar problemas en tiempo real y actuar en consecuencia (cargar un recurso alternativo, registrar el error, etc.).

---

# 🟦 **7. abort**

Este evento ocurre cuando la carga de un recurso **se detiene repentinamente**, ya sea porque:

- se canceló manualmente,
    
- el usuario cambió de página,
    
- la conexión se cortó,
    
- el navegador decidió abortarla.
    

Suele usarse para detectar **interrupciones en imágenes o recursos multimedia**.

```js
img.addEventListener("abort", () => {
  console.log("La carga fue interrumpida.");
});
```

---

# 🟦 **8. select**

Este evento se ejecuta cuando el usuario **selecciona texto dentro de un input** o textarea.

Es muy útil cuando:

- se quiere detectar selección para copiar
    
- se necesita mostrar información al seleccionar texto
    
- se implementan herramientas de edición de texto
    

```js
input.addEventListener("select", () => {
  console.log("Texto seleccionado dentro del input.");
});
```

---

# 🟦 **9. toggle (para `<details>`)**


El evento `toggle` se dispara cuando un elemento `<details>`:

- se abre, o
    
- se cierra
    

Es decir, detecta el **cambio de estado del elemento**.

Muy útil para crear:

- menús plegables
    
- secciones de FAQ
    
- detalles colapsables sin JavaScript adicional
    

```js
details.addEventListener("toggle", () => {
  console.log("El elemento <details> cambió de estado.");
});
```

---

Los UI Events monitorean:

- el ciclo de carga del documento
    
- cambios en la interfaz
    
- comportamiento global de la ventana
    
- condiciones de error o interrupción
    
- eventos que afectan al documento entero
    

No son micro-interacciones (como mouse o teclado), sino **macro-eventos que afectan al entorno completo**.

---
