# Guía explicativa: `alert`, `confirm` y `prompt` en JavaScript

En JavaScript existen tres funciones nativas que permiten mostrar ventanas emergentes al usuario y, de forma muy básica, interactuar con él: `alert`, `confirm` y `prompt`. Estas funciones aparecen directamente en el navegador sin necesidad de crear elementos en HTML, y fueron durante muchos años la manera principal de mostrar mensajes o pedir datos.

Aunque hoy en día casi no se utilizan en proyectos reales, entenderlas es fundamental porque representan los primeros pasos de la interacción entre un programa en JavaScript y la persona que lo usa.

---

## `alert()`

El método `alert` sirve para **mostrar un mensaje informativo** en pantalla.  
Cuando lo ejecutamos, el navegador abre una pequeña ventana emergente con el texto que le indiquemos y un único botón (generalmente “Aceptar” o “OK”). Mientras esa ventana está abierta, todo el resto de la página queda bloqueado; es decir, el usuario no puede hacer nada más hasta que cierre la alerta.

Su uso más común es para dar avisos o notificaciones rápidas. Por ejemplo:

```js
alert("Bienvenido a nuestra página");
```

Al ejecutar este código, aparece un cuadro con ese mensaje y un botón para cerrarlo. No devuelve ningún valor; simplemente se limita a mostrar el texto.

En su momento era muy útil para depurar o mostrar mensajes urgentes, pero hoy se considera intrusivo. En lugar de usarlo para producción, se prefiere `console.log()` o notificaciones más modernas. Aun así, `alert` sigue siendo una herramienta práctica para aprender o hacer pruebas rápidas.

---

## `confirm()`

Si `alert` solo informa, `confirm` nos permite **hacer una pregunta cerrada al usuario** y obtener una respuesta de “sí” o “no”.

Cuando usamos `confirm`, el navegador muestra un cuadro de diálogo con un mensaje y dos botones: “Aceptar” y “Cancelar”. El aspecto de esa ventana depende del navegador y del sistema operativo, pero el comportamiento siempre es el mismo:

- Si el usuario hace clic en **Aceptar**, la función devuelve `true`.
    
- Si el usuario hace clic en **Cancelar**, presiona la tecla Esc o cierra la ventana, la función devuelve `false`.
    

Esto nos permite tomar decisiones dentro del programa según lo que haya elegido la persona.

Ejemplo sencillo:

```js
let decision = confirm("¿Deseas continuar?");
if (decision) {
  alert("Elegiste continuar.");
} else {
  alert("Cancelaste la acción.");
}
```

En este caso, el flujo del programa cambia dependiendo de la respuesta. Este es el gran aporte de `confirm`: transformar la elección del usuario en un valor booleano que podemos usar en condiciones.

Un detalle importante es que `confirm`, al igual que `alert`, **bloquea la ejecución** del código hasta que el usuario responde. Esto significa que el programa se “pausa” en ese punto. Por esa razón, en aplicaciones modernas no se suele usar, ya que genera una experiencia poco agradable, pero para aprender es muy útil porque nos enseña cómo tomar decisiones basadas en la interacción del usuario.

---

## `prompt()`

La tercera función, `prompt`, nos permite ir un paso más allá: **pedir información escrita al usuario**.

Cuando se ejecuta, aparece una ventana emergente con un mensaje y un cuadro de texto en el que la persona puede escribir lo que quiera. Además, incluye dos botones: “Aceptar” y “Cancelar”.

El valor que devuelve `prompt` depende de lo que haga el usuario:

- Si escribe algo y pulsa **Aceptar**, devuelve ese texto como cadena (`string`).
    
- Si pulsa **Aceptar** pero deja el cuadro vacío, devuelve una cadena vacía (`""`).
    
- Si pulsa **Cancelar** o cierra la ventana, devuelve `null`.
    

Veamos un ejemplo:

```js
let nombre = prompt("¿Cómo te llamas?");
if (nombre === null) {
  alert("No ingresaste tu nombre.");
} else {
  alert("Hola, " + nombre);
}
```

En este caso, el programa distingue entre cancelar y aceptar. Incluso podemos dar un **valor por defecto** que aparecerá escrito en el cuadro de texto al abrirse:

```js
let edad = prompt("Ingresa tu edad:", "18");
alert("Tu edad es " + edad);
```

Esto es útil cuando queremos sugerir una respuesta inicial.

Al igual que los otros dos métodos, `prompt` también bloquea la página hasta que el usuario responde. Además, siempre devuelve texto; si queremos números, tenemos que convertirlos manualmente (`Number()`, `parseInt()`, etc.).

---

## Comparación y conclusión

- **`alert`**: solo muestra un mensaje. No devuelve nada útil.
    
- **`confirm`**: pregunta al usuario y devuelve un booleano (`true` o `false`).
    
- **`prompt`**: pide un dato y devuelve un texto, o `null` si el usuario cancela.
    

Los tres son modales nativos del navegador y tienen la ventaja de ser extremadamente sencillos de usar. Sin embargo, también tienen desventajas: bloquean la interacción, no se pueden personalizar y generan una experiencia poco amigable en sitios modernos.

Por eso, en proyectos reales suelen reemplazarse con **formularios** o **modales personalizados** hechos con HTML, CSS y JavaScript. Aun así, conocer `alert`, `confirm` y `prompt` es fundamental porque representan la base de la interacción en JavaScript y todavía se utilizan en ejemplos, en cursos introductorios y en pruebas rápidas.

---
