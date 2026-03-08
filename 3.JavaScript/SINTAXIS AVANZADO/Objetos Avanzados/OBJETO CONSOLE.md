# 🌐 Introducción profunda al objeto `window`

El objeto `window` es la **raíz del entorno de ejecución del navegador**. No es simplemente un contenedor de métodos: representa la **ventana del navegador en sí misma**, y funciona como el **objeto global** del lenguaje dentro del contexto del navegador. Esto significa que cualquier variable global, función o estructura declarada sin un espacio de nombres explícito pasa a formar parte de `window`.

Desde un punto de vista conceptual, `window` integra:

- El **DOM (Document Object Model)**, encargado de la representación estructural del documento HTML.
    
- El **BOM (Browser Object Model)**, que expone elementos propios del navegador (historial, barra de direcciones, tamaño de ventana, etc.).
    
- El sistema de **eventos** heredado de `EventTarget`, lo que lo convierte en un objeto capaz de registrar, despachar y manejar eventos globales.
    

Por esa razón, muchas APIs esenciales como `alert`, `setTimeout`, `localStorage` o `fetch` están alojadas dentro del objeto `window`.

Ejemplo básico:

```js
console.log(window === this); // true en contexto global
```

---

# ✔ Relación con `EventTarget` (mención técnica breve)

`window` hereda de `EventTarget`, lo que lo habilita como **receptor y emisor de eventos globales**. Esto implica que puede escuchar eventos como:

- `load`
    
- `scroll`
    
- `resize`
    
- `visibilitychange`
    
- `keydown`, etc.
    

Gracias a esta herencia se puede escribir:

```js
window.addEventListener("scroll", () => {
  console.log("El documento se está desplazando");
});
```

Más adelante se desarrollará `EventTarget` en profundidad, incluyendo fases de propagación, bubbling, captura y el sistema de event listeners.

---

# ⚙️ Métodos fundamentales de `window` (conceptualmente desarrollados)

### `open()`

Este método permite **cargar un nuevo recurso dentro de un contexto de navegación**. Puede abrirse una nueva pestaña, una nueva ventana o incluso reemplazar la página actual, dependiendo de los argumentos.

Su propósito original era crear ventanas emergentes controladas por JavaScript. Hoy está fuertemente restringido por políticas del navegador para evitar spam y popups abusivos.

Ejemplo con parámetros:

```js
window.open("https://ejemplo.com", "NuevaVentana", "width=800,height=600");
```

Conceptualmente: permite controlar navegación programática.

---

### `close()`

Cierra la ventana desde la cual se ejecuta la llamada.  
Por seguridad, sólo puede cerrar ventanas **abiertas mediante `open()`**, no pestañas normales.

---

### `closed`

Propiedad booleana que indica si una referencia a `window` ya no está activa.  
Es extremadamente útil para verificar ventanas auxiliares abiertas con scripts.

Ejemplo:

```js
let popup = open("...");
console.log(popup.closed); // false o true
```

---

### `name`

Define un **identificador simbólico** para la ventana.  
Históricamente se utilizaba para cargar documentos en frames o para enviar formularios apuntando a ventanas específicas. Aunque hoy se usa poco, aún forma parte de la especificación.

---

### `stop()`

Detiene el **flujo de carga actual** de la página. Se comporta como presionar manualmente el botón de detener carga en el navegador.  
No detiene scripts ya cargados, pero evita que continúen las descargas.

---

### `alert()`

Muestra un cuadro modal nativo diseñado para interacción mínima.  
Bloquea toda la ejecución de eventos mientras el cuadro esté abierto.  
No debe abusarse en UI moderna, pero sigue siendo útil para pruebas rápidas.

---

### `print()`

Fuerza la apertura del cuadro de impresión del navegador.  
Se utiliza cuando se generan documentos dinámicos que deben imprimirse.

---

### `prompt()`

Abre un cuadro de diálogo con una barra de entrada y el texto proporcionado.  
Devuelve un `string` o `null` si se cancela.  
Se utiliza para capturar entradas rápidas sin construir UI adicional.

---

### `confirm()`

Muestra un cuadro modal con dos botones: **Aceptar** y **Cancelar**, devolviendo `true` o `false`.  
Es útil para validaciones previas a operaciones críticas.

---

# 🖥️ Propiedades vinculadas a desplazamiento y posición

### `scrollX` y `scrollY`

Devuelven la cantidad total de desplazamiento que se ha aplicado al documento desde su origen superior izquierdo.

Es información importante para efectos visuales, animaciones, carga diferida de recursos, etc.

---

### `scroll()`

Permite desplazar el viewport a una coordenada absoluta.  
Puede utilizarse con números o con un objeto de configuración moderno:

```js
scroll({ top: 1000, behavior: "smooth" });
```

---

# 🪟 Métodos de control de la ventana física

Estos métodos existen en el estándar, pero hoy están restringidos por políticas de seguridad:

- `moveTo()` → posiciona la ventana en coordenadas absolutas
    
- `moveBy()` → mueve la ventana sumando desplazamiento
    
- `resizeTo()` → reajusta el tamaño de la ventana a medidas específicas
    
- `resizeBy()` → redimensiona la ventana basándose en diferencias numéricas
    
- `minimize()` → intenta minimizar la ventana
    

Sólo funcionan si la ventana fue creada por script.

---

# 📊 **Propiedades del objeto `screen` (COMPLETO Y DESARROLLADO)**

`screen` representa la **pantalla física en la que se está mostrando la ventana**.  
Es parte del BOM y no del DOM.

Su objetivo es proporcionar información sobre la **resolución física y el rango disponible de visualización**, lo cual permite adaptar interfaces y comportamientos dinámicos.

## Propiedades principales

### `screen.width`

Devuelve el **ancho total de la pantalla física en píxeles**.

### `screen.height`

Devuelve la **altura total** de la pantalla física.

> Son medidas de resolución, no del viewport.  
> Si tu monitor es FULL HD: width = 1920, height = 1080.

---

### `screen.availWidth`

Indica el ancho disponible para usar **sin contar elementos reservados por el sistema operativo**, como la barra de tareas.

---

### `screen.availHeight`

Devuelve lo mismo que `availWidth` pero en sentido vertical.  
Permite saber cuántos píxeles son realmente utilizables.

---

### `screen.colorDepth`

Indica la **profundidad de color** en bits por píxel utilizada por la pantalla.  
Valores comunes: 24 bits (16 millones de colores), 32 bits (con alfa).

---

### `screen.pixelDepth`

Similar a `colorDepth`, pero considera la profundidad real del sistema para representar un píxel.  
Generalmente coincide con `colorDepth`.

---

### `screen.orientation`

Devuelve un objeto que describe la **orientación actual del dispositivo**, por ejemplo:

- `"landscape-primary"`
    
- `"portrait-primary"`
    

Permite reaccionar dinámicamente ante cambios:

```js
screen.orientation.addEventListener("change", () =>
  console.log("Se giró la pantalla")
);
```

---

## Propósito funcional del objeto `screen`

El objetivo es permitir:

- Adaptación visual según la resolución real del usuario.
    
- Interfaces multiplataforma.
    
- Detección de cambios de orientación en dispositivos móviles.
    
- Implementaciones avanzadas de **pantalla completa**, video o juegos web.
    

---

# 🧭 Objetos barprop (contexto histórico)

Los objetos `menubar`, `toolbar`, `statusbar`, etc., exponen información sobre la existencia de componentes visuales del navegador.  
Hoy su utilidad es prácticamente nula debido a restricciones de seguridad y la estandarización de las UI modernas.

---
# 🌍 Objeto `window.location` (Desarrollo completo)

`window.location` es una **interfaz que representa la URL actual de la ventana** y permite tanto **leer información detallada** de la dirección en la que estamos, como **modificarla**, provocando una navegación programática.

Es uno de los componentes fundamentales del **BOM (Browser Object Model)** y forma parte de `window`.

Desde un punto de vista conceptual, `location` funciona como un **parser de URLs**, proporcionando cada parte de la dirección en propiedades separadas.

---

## 🔹 Propiedades principales de `location`

### `location.href`

- Representa la **URL completa** en formato string.
    
- Es la propiedad **más importante**.
    
- Puede leerse o escribirse.
    
- Si se modifica, **redirige inmediatamente** a la página especificada.
    

Ejemplo:

```js
console.log(location.href); 
location.href = "https://google.com";
```

---

### `location.protocol`

- Devuelve el protocolo utilizado por la página.
    
- Incluye los dos puntos.
    

Ejemplos típicos:

```
"https:"
"http:"
"file:"
```

Esta propiedad es útil para verificar si una web está bajo HTTPS.

---

### `location.hostname`

- Devuelve el **nombre del dominio**, sin protocolo ni rutas.
    
- No incluye puerto.
    

Ejemplo:

```
"www.ejemplo.com"
```

---

### `location.host`

- Similar a `hostname`, pero **incluye el puerto** (si existe uno explícito).
    

Ejemplo:

```
"localhost:3000"
"www.ejemplo.com:8080"
```

---

### `location.port`

- Devuelve el puerto de la URL **como string**.
    
- Si la URL usa el puerto estándar del protocolo (443 en HTTPS, 80 en HTTP), devuelve cadena vacía.
    

---

### `location.pathname`

- Devuelve la **ruta interna del sitio**, incluyendo barras iniciales.
    

Ejemplos:

```
"/productos/lista"
"/"
"/index.html"
```

No incluye dominio, protocolo ni parámetros.

---

### `location.search`

- Devuelve la **cadena de consulta completa**, incluyendo el signo `?`.
    

Ejemplo:

```
"?user=ivan&id=25&modo=dark"
```

Esta propiedad es clave para trabajar con parámetros dinámicos.  
Puede ser procesada con `URLSearchParams`.

---

### `location.hash`

- Devuelve el fragmento de documento (ancla) que se encuentra después del signo `#`.
    

Ejemplo:

```
"#seccion3"
```

⚠ Importante:  
Cambiar un hash **no recarga la página**, lo que lo hace útil para navegación interna en SPA.

---

### `location.origin`

- Devuelve la **combinación protocol + host + puerto** en una sola cadena.
    

Ejemplo:

```
"https://midominio.com:8080"
```

Es una propiedad **sólo de lectura** y muy útil cuando se trabaja con Web APIs que exigen “mismo origen”.

---

## 🔹 Métodos asociados a `location`

Además de sus propiedades, `location` posee métodos que permiten controlar la navegación.

---

### `location.assign(url)`

Carga una nueva página, de forma equivalente a cambiar `href`, pero más explícito semánticamente.

```js
location.assign("https://youtube.com");
```

---

### `location.replace(url)`

Navega hacia otra página **sin guardar la actual en el historial**.  
Esto impide que el usuario vuelva atrás usando “atrás”.

Usado cuando se quiere **reemplazar** la ruta actual:

```js
location.replace("/login");
```

---

### `location.reload(forceReload)`

Recarga la página actual:

- Sin parámetros → recarga desde caché.
    
- Con `true` → fuerza recarga desde el servidor.
    

Ejemplo:

```js
location.reload(true);
```

---

## 🔹 Relación con el historial del navegador

`location` y `history` trabajan juntos:

- `location` controla **qué página se carga**.
    
- `history` controla **cómo se registra esa navegación**.
    

Por eso `replace()` no genera historial y `assign()` sí.

---

## 🔹 Ejemplo de descomposición completa de una URL

Si la URL es:

```
https://www.ejemplo.com:8080/productos/lista?page=2#ofertas
```

Entonces:

|Propiedad|Valor|
|---|---|
|href|`"https://www.ejemplo.com:8080/productos/lista?page=2#ofertas"`|
|protocol|`"https:"`|
|host|`"www.ejemplo.com:8080"`|
|hostname|`"www.ejemplo.com"`|
|port|`"8080"`|
|pathname|`"/productos/lista"`|
|search|`"?page=2"`|
|hash|`"#ofertas"`|
|origin|`"https://www.ejemplo.com:8080"`|

---

# 📌 Importancia conceptual

El objeto `location` es esencial para:

- Redirecciones programáticas
    
- Trabajar con parámetros dinámicos de URL
    
- Implementar navegación en SPAs sin recargar la página
    
- Validar origen, protocolo, puertos y rutas
    
- Consultar el estado actual de la ubicación desde scripts
    

Comprender `location` implica entender **cómo una página llega a ser cargada y cómo puede ser manipulada en tiempo real por JavaScript**.

---
