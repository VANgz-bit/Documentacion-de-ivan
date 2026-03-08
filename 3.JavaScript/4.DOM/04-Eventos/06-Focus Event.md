# ⭐ **FOCUS EVENTS **

Los **focus events** forman una categoría del DOM destinada a manejar **el estado de enfoque** (focus) dentro de un documento HTML.  
El objetivo es permitir que los desarrolladores controlen **qué elemento está activo**, **cómo se mueve el foco**, y **cómo responde la interfaz cuando el usuario interactúa usando el teclado, el mouse o la navegación por accesibilidad**.

Son eventos esenciales para:

- formularios
    
- accesibilidad (personas que no usan mouse)
    
- navegación por teclado
    
- componentes UI como modales, menús, tooltips, dropdowns
    
- validación de campos
    
- manejo de focus programático
    

---

# ⭐ **1. ¿Qué es exactamente el “focus”? 

En términos del DOM, **el focus es el estado que determina a qué elemento se le envían las interacciones de teclado**.

Cuando un elemento tiene el foco:

1. recibe inmediatamente la **entrada del teclado**  
    (lo que tipeas va allí)
    
2. responde a las **teclas especiales** (Enter, Escape, Tab, Space)
    
3. se convierte en el **punto de interacción principal** del usuario
    
4. obtiene una **relación directa con el motor de accesibilidad** del navegador
    
5. participa en el sistema de **navegación secuencial** de la página (TAB order)
    

En HTML, no todos los elementos pueden tener focus naturalmente, porque el navegador define cuáles elementos son interactivos por diseño.

---

# ⭐ **2. Elementos que pueden recibir focus **

## ✔ **Elementos focusables por defecto**

Son elementos cuyo propósito es interactuar:

- `<input>`
    
- `<textarea>`
    
- `<button>`
    
- `<select>`
    
- `<a href="…">`
    
- `<details>`
    
- `<iframe>`
    
- controles nativos del navegador
    

Estos ya están integrados en el sistema de enfoque.

## ✔ **Elementos que pueden recibir focus manualmente**

Cualquier elemento del DOM puede convertirse en “focusable” si se define:

```html
<div tabindex="0"></div>
```

El atributo `tabindex` determina:

- si puede recibir focus
    
- si puede ser navegado con TAB
    
- en qué orden aparece
    

Esto es importante para componentes modernos que crean botones custom, dropdowns o elementos que se comportan como controles pero no son nativos.

---

# ⭐ **3. El conjunto de eventos que forman la API de Focus Events**

Los eventos principales son **cuatro**, divididos en dos pares:

---

## ⭐ **(A) focus y blur — NO burbujean**

### **1. focus**

Se dispara cuando un elemento **obtiene el enfoque**.

Ejemplos concretos:

- el usuario hace click en un input
    
- el usuario navega con TAB
    
- el focus se asigna con JavaScript (`element.focus()`)
    

Es un evento muy preciso y directo: siempre apunta al elemento que se activa.

### **2. blur**

Se dispara cuando un elemento **pierde el enfoque**.

Sucede cuando:

- el usuario pasa al siguiente campo
    
- hace click fuera
    
- el foco se mueve programáticamente (`element.blur()`)
    

---

## ⭐ **(B) focusin y focusout — SÍ burbujean**

Estos eventos existen para facilitar el manejo del focus “desde arriba” en el DOM.

### **3. focusin**

Es igual a _focus_, pero **sí burbujea**.

Esto significa que:

- puedes escuchar todos los cambios de foco desde un contenedor
    
- no necesitas agregar listeners uno por uno
    
- puedes detectar cuándo cualquier elemento dentro del contenedor obtiene focus
    

### **4. focusout**

Es igual a _blur_, pero **sí burbujea**.

Muy útil para:

- validar campos dentro de un formulario
    
- mostrar errores
    
- detectar cuándo el usuario abandona un elemento cargado dinámicamente
    

---

# ⭐ **4. ¿Por qué focus/blur NO burbujean, pero focusin/focusout sí?**

La razón es conceptual y técnica:

- **focus** y **blur** son estados íntimamente ligados al _elemento específico_.  
    El navegador define que el “estado de enfoque” no se propaga hacia los padres.
    
- Sin embargo, en interfaces complejas, se necesita observar cambios de foco _globales_.  
    Por eso se crearon **focusin** y **focusout**, que sí burbujean.
    

Esto da dos comportamientos complementarios:

- focus/blur → nivel puntual (elemento exacto)
    
- focusin/focusout → nivel global (contenedor, formulario, documento)
    

Ambos modelos son útiles según el tipo de UI.

---

# ⭐ **5. ¿Cómo se comportan en el flujo del DOM? **

Todos los eventos del DOM tienen dos posibles fases:

- **capturing (captura)**
    
- **bubbling (burbujeo)**
    

Pero los Focus Events son especiales:

|Evento|Captura|Bubujeo|Nota|
|---|---|---|---|
|**focus**|✔|❌|NO burbujea|
|**blur**|✔|❌|NO burbujea|
|**focusin**|✔|✔|burbujea|
|**focusout**|✔|✔|burbujea|

Esto los hace más flexibles.

---

# ⭐ **6. El objeto FocusEvent**

Cada vez que ocurre un Focus Event, el navegador genera un objeto de tipo **FocusEvent**, que extiende a **UIEvent**, que a su vez extiende a **Event**.

Las propiedades importantes son:

---

## ✔ **event.target**

El elemento que obtiene o pierde focus.

### Ejemplo:

- Si un input gana el foco → `target` es el input
    
- Si un input pierde foco → `target` es el input que lo perdió
    

---

## ✔ **event.relatedTarget** (la clave del sistema)

Esta es la propiedad más importante de FocusEvent.

Indica:

- en _focus_: desde dónde viene el foco
    
- en _blur_: hacia dónde va el foco
    
- en _focusin/focusout_: elemento previo o siguiente del proceso
    

Es decir, te muestra la **transición** entre elementos.

Ejemplo:

```js
email.addEventListener("blur", (e) => {
  console.log("Siguiente elemento:", e.relatedTarget);
});
```

Esto permite saber **hacia dónde se mueve el foco**, algo vital en accesibilidad y validación.

---

# ⭐ **7. ¿Por qué los Focus Events son esenciales en desarrollo moderno?**

Los Focus Events permiten:

### ✔ Accesibilidad

Los usuarios que navegan con teclado **dependen completamente del focus**.  
Si el focus no está bien manejado, la página se vuelve inutilizable.

### ✔ Formularios inteligentes

Podés validar por campo y no esperar a enviar el formulario.

### ✔ Componentes interactivos

Muchos elementos modernos (dropdowns, menús, autocompletados) dependen del focus para abrirse, cerrarse o navegarse.

### ✔ Control de interfaces complejas

Un modal o una ventana flotante debe:

- atrapar el foco
    
- devolver el foco al elemento original
    
- bloquear el focus fuera del modal
    

### ✔ UX profesional

El focus correcto evita que el usuario se pierda o interactúe con elementos invisibles.

---

# ⭐ **8. Ejemplo EXTENDIDO de uso real**

Supongamos un formulario:

```html
<form id="form">
  <input id="usuario" placeholder="Usuario">
  <input id="email" placeholder="Email">
  <input id="pass" placeholder="Contraseña">
</form>
```

### Usar focusin para escuchar todos los cambios dentro del form:

```js
form.addEventListener("focusin", (event) => {
  console.log("Elemento que recibió focus:", event.target);
});
```

### Usar focusout para validación:

```js
form.addEventListener("focusout", (event) => {
  if(event.target.value === ""){
    console.log("El campo está vacío:", event.target);
  }
});
```

Esto captura **cualquier** input dentro del formulario sin necesidad de agregar listeners individuales.

---

# ⭐ **9. Resumen final 

- Focus Events es la categoría del DOM que maneja **el estado de enfoque** entre elementos.
    
- El foco determina **dónde va el teclado** y **qué elemento está activo**.
    
- Los eventos principales son:  
    **focus**, **blur**, **focusin**, **focusout**.
    
- focus/blur no burbujean; focusin/focusout sí.
    
- El objeto `FocusEvent` trae propiedades clave, especialmente **relatedTarget**.
    
- Son fundamentales para formularios, accesibilidad, y componentes UI modernos.
    

---
