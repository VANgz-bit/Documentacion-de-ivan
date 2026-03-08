# **Eventos de teclado (Keyboard Events) — Explicación completa y desarrollada**

Los eventos de teclado representan las interacciones del usuario con el teclado físico. El navegador detecta cuándo una tecla es presionada, mantenida o soltada, y genera eventos específicos que pueden capturarse para crear comportamientos interactivos dentro de una página web.

Estos eventos son fundamentales para tareas como:

- Formularios inteligentes
    
- Accesos rápidos y atajos de teclado
    
- Juegos en el navegador
    
- Navegación accesible
    
- Validaciones instantáneas
    

---

# **1. Tipos principales de eventos de teclado**

## **1. `keydown`**

Se ejecuta **cuando una tecla es presionada** hacia abajo.  
Es el evento más utilizado porque detecta absolutamente todas las teclas, incluidas las especiales (Shift, Ctrl, Alt, Tab, F1-F12, etc.).

**Características importantes:**

- Se dispara continuamente si se mantiene la tecla apretada (repetición automática).
    
- Ideal para atajos de teclado o juegos.
    

---

## **2. `keypress` (obsoleto)**

Este evento detectaba cuando una tecla producía un “carácter imprimible”.  
Hoy está en proceso de eliminación, por lo que **no se recomienda usarlo**.

---

## **3. `keyup`**

Se ejecuta **cuando la tecla es soltada**.  
Es útil para validar datos luego de que el campo queda actualizado.

Por ejemplo:

- Validaciones de campos de texto
    
- Actualizaciones en tiempo real
    
- Detección del fin de un comando (soltar Control)
    

---

# **2. Propiedades más importantes del objeto de evento (KeyboardEvent)**

Cuando se dispara un evento de teclado, el navegador crea un objeto de tipo **KeyboardEvent**, que contiene información detallada sobre la tecla presionada.

A continuación se desarrollan las propiedades principales:

---

## **2.1 `key`**

Devuelve **el valor de la tecla presionada**, tal como se interpreta en el contexto actual del teclado.

Ejemplos:

- Presionar “a” devuelve `"a"`.
    
- Presionar “A” devuelve `"A"` (si Shift está activo).
    
- Presionar “Enter” devuelve `"Enter"`.
    
- Flecha izquierda devuelve `"ArrowLeft"`.
    

Esta propiedad es ideal para lógica semántica, ya que devuelve el carácter final.

---

## **2.2 `code`**

Devuelve **el código físico de la tecla** en el teclado, independientemente del idioma o distribución.

Ejemplos:

- `"KeyA"` siempre corresponde a la tecla A.
    
- `"Digit1"` representa el número 1 de la fila superior.
    
- `"Space"` representa la barra espaciadora.
    

Esto es útil cuando se necesita detectar teclas específicas sin importar el idioma del teclado.

---

## **2.3 `keyCode` (obsoleto pero aún funcional)**

Devuelve un **número** asociado a la tecla.

Ejemplos:

- Enter = 13
    
- Escape = 27
    

Ya no se recomienda usarlo, pero sigue apareciendo en muchos códigos antiguos.

---

## **2.4 `altKey`, `ctrlKey`, `shiftKey`, `metaKey`**

Indican si se está presionando una tecla modificadora en el momento del evento.

Estas propiedades devuelven un valor booleano (`true` o `false`).

Ejemplos:

- `event.shiftKey === true` si Shift está presionado.
    
- `event.ctrlKey` se usa para detectar combinaciones como Ctrl + S.
    
- `event.metaKey` es la tecla Windows en PC y Command en Mac.
    

---

## **2.5 `repeat`**

Indica si el evento se disparó automáticamente por mantener la tecla presionada.

- `false` → primera vez que se presiona
    
- `true` → evento repetido automáticamente
    

Muy útil en videojuegos o para bloquear repeticiones indeseadas.

---

## **2.6 `isComposing`**

Indica si el usuario está usando un **método de entrada complejo**, como la escritura de idiomas asiáticos.

---

# **3. Métodos del evento**

Además de las propiedades, existen métodos del evento que permiten controlar el comportamiento del navegador.

---

## **3.1 `preventDefault()`**

Impide que el navegador realice la **acción por defecto** asociada a una tecla.

Ejemplos:

- Evitar que “Backspace” retroceda a la página anterior.
    
- Bloquear el scroll que produce la tecla “Space”.
    
- Impedir enviar un formulario cuando se presiona Enter.
    

Se usa en la mayoría de aplicaciones web interactivas.

---

## **3.2 `stopPropagation()`**

Evita que el evento se **propague** hacia elementos padres.

Esto permite controlar exactamente qué elemento responde a la acción.

---

## **3.3 `stopImmediatePropagation()`**

Detiene la propagación **y además** evita que otros listeners en el mismo elemento se ejecuten.

Es una versión más estricta que `stopPropagation()`.

---

# **4. Ejemplos desarrollados**

### **Ejemplo 1 — Detectar teclas simples**

```js
document.addEventListener("keydown", (event) => {
    console.log("Tecla presionada:", event.key);
    console.log("Código físico:", event.code);
});
```

---

### **Ejemplo 2 — Detectar combinación de teclas**

```js
document.addEventListener("keydown", (event) => {
    if (event.ctrlKey && event.key === "s") {
        event.preventDefault();
        console.log("Atajo Ctrl + S detectado.");
    }
});
```

---

### **Ejemplo 3 — Evitar la repetición automática**

```js
document.addEventListener("keydown", (event) => {
    if (event.repeat) return; 
    console.log("Primera vez que presiona:", event.key);
});
```

---

### **Ejemplo 4 — Validación de input**

```js
input.addEventListener("keyup", (event) => {
    console.log("Valor actualizado:", event.target.value);
});
```

---

# **5. Resumen conceptual**

- **keydown**: se activa cuando la tecla baja → detecta todas las teclas.
    
- **keyup**: se activa cuando la tecla se suelta → ideal para validaciones.
    
- **KeyboardEvent** da acceso a información clave:
    
    - `key`: valor final de la tecla
        
    - `code`: posición física
        
    - `shiftKey`, `ctrlKey`, etc.: modificadores
        
    - `repeat`: repetición automática
        
- Métodos importantes:
    
    - `preventDefault()`
        
    - `stopPropagation()`
        
    - `stopImmediatePropagation()`
        

---
