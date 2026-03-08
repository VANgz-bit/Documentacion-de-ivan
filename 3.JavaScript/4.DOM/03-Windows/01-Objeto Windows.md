# 🌐 Introducción al objeto `window`

En JavaScript, `window` representa la **ventana o pestaña del navegador** donde se está ejecutando nuestro documento web. Es el objeto global más importante en el contexto del navegador, ya que **contiene todo lo necesario para trabajar con el DOM, la URL, los eventos, la interfaz del navegador, temporizadores, historial, etc.**

Todo lo que no está dentro de otro objeto, pertenece implícitamente a `window`. Por ejemplo, cuando escribimos:

```js
alert("Hola")
```

En realidad estamos ejecutando:

```js
window.alert("Hola")
```

---

## 📌 Relación con EventTarget (mención breve)

`window` **hereda las propiedades de `EventTarget`**, lo que significa que puede **escuchar y manejar eventos**, como `click`, `load`, `scroll`, `resize`, etc.

Más adelante veremos EventTarget en profundidad; por ahora alcanza con saber que gracias a esto podemos hacer:

```js
window.addEventListener("resize", () => console.log("Cambió el tamaño"));
```

---

# ⚙️ Métodos principales de `window`

### `open()`

Carga un recurso en el contexto de navegación. Puede:

- Abrir una **nueva pestaña o ventana**.
    
- Cargar una URL **en la misma ventana**, dependiendo de los parámetros.
    

Ejemplo:

```js
window.open("https://google.com", "_blank");
```

---

### `close()`

Cierra la ventana actual o una referencia abierta previamente con `window.open`.

---

### `closed`

No es un método, sino una **propiedad booleana** que indica si la ventana referenciada está cerrada.

---

### `name`

Propiedad que **obtiene o establece el nombre de la ventana**. Se utiliza para identificarla cuando se hacen cargas desde otras ventanas.

---

### `stop()`

Detiene la carga actual de recursos (similar a presionar “X” en la barra de carga del navegador).

---

### `alert()`

Muestra un cuadro de diálogo modal con un mensaje y un botón "Aceptar".  
Bloquea la interacción de la página hasta que se cierre.

---

### `print()`

Abre el cuadro de diálogo del sistema operativo para **imprimir la página actual**.

---

### `prompt()`

Muestra un cuadro de diálogo con un mensaje y un input.  
Devuelve lo que el usuario escribió o `null` si canceló.

Ejemplo:

```js
let nombre = prompt("¿Cuál es tu nombre?");
```

---

### `confirm()`

Muestra un cuadro de diálogo con un mensaje y **dos botones**: Aceptar y Cancelar.  
Devuelve `true` o `false`.

```js
if (confirm("¿Seguro que quieres salir?")) {
  // ...
}
```

---

# 🖥️ Propiedades relacionadas a la pantalla 🪟

Estas propiedades devuelven mediciones sobre **la posición y el desplazamiento**, tanto del documento como de la ventana respecto a la pantalla.

### `screen`

Devuelve un objeto con información del **monitor**, como resolución, profundidad de color, etc.

---

### `screenLeft` y `screenTop`

Devuelven la distancia **entre la ventana del navegador y los bordes de la pantalla**.

- `screenLeft`: distancia horizontal
    
- `screenTop`: distancia vertical
    

---

### `scrollX` y `scrollY`

Devuelven la cantidad de píxeles que se ha desplazado el **documento**:

- `scrollX` → desplazamiento horizontal
    
- `scrollY` → desplazamiento vertical
    

Son muy usados para detectar scroll:

```js
window.addEventListener("scroll", () => {
  console.log(window.scrollY);
});
```

---

### `scroll()`

Permite desplazar la ventana hacia una posición específica.

Acepta:

- Coordenadas absolutas:
    

```js
scroll(0, 500)
```

- Un objeto con opciones, por ejemplo:
    

```js
scroll({
  top: 800,
  behavior: "smooth"
})
```

---

# 🪟 Métodos de movimiento y tamaño de ventana

Estos métodos **solo funcionan en ventanas abiertas por JavaScript** (no en pestañas normales por restricciones de seguridad):

### `minimize()`

Minimiza la ventana.

### `resizeBy()`

Cambia el tamaño de la ventana **sumando o restando medidas**.

### `resizeTo()`

Establece directamente un **nuevo tamaño absoluto** para la ventana.

### `moveBy()`

Mueve la ventana una distancia relativa (suma o resta posiciones).

### `moveTo()`

Ubica la ventana en coordenadas absolutas dentro de la pantalla.

---

# 🧭 Objetos de la barra del navegador (barprop)

El objeto `window` contiene referencias a los elementos visibles del navegador. Estos objetos permiten saber si ciertos elementos existen o están visibles.

Ejemplos:

- `locationbar`
    
- `menubar`
    
- `personalbar`
    
- `scrollbars`
    
- `statusbar`
    
- `toolbar`
    

Hoy en día NO se suelen manipular por políticas de seguridad del navegador, pero forman parte del estándar histórico.

---

# 🔗 Propiedades importantes de `window.location`

El objeto `location` describe completamente la **URL actual**.

Ejemplos:

- `window.location.href` → Devuelve o cambia la URL completa.
    
- `window.location.hostname` → Dominio del sitio.
    
- `window.location.pathname` → Ruta del archivo dentro del sitio.
    
- `window.location.protocol` → Protocolo (`https:`, `http:`, etc).
    

📌 Cambiar `location.href` redirige la página:

```js
window.location.href = "https://youtube.com";
```

---

# ¿Por qué es importante entender `window`?

Porque es el **punto de entrada del entorno web**.  
Controlar `window` es controlar:

- La navegación
    
- Los diálogos del navegador
    
- El tamaño y posición de la ventana
    
- El scroll
    
- Los eventos globales
    
- La URL y el historial
    

Todo lo demás (DOM, BOM, eventos, storage, etc.) depende directa o indirectamente de este objeto.

---

