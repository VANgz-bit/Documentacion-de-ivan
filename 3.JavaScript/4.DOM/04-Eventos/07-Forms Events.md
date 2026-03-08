# **Eventos de Formulario (Form Events)**

Los _eventos de formulario_ son los que se activan mientras una persona interactúa con elementos como `<form>`, `<input>`, `<select>`, `<textarea>` y `<button>`.  
Son fundamentales para validar datos, controlar envíos, reaccionar a cambios y manejar procesos de ingreso de información.

A continuación se explican los principales, con definiciones ampliadas y claras.

---

## **1. `submit`**

Se activa cuando un formulario intenta enviarse, ya sea por:

- Presionar un botón `type="submit"`
    
- Presionar Enter dentro de un input
    
- Llamar manualmente a `form.submit()`
    

**Para qué sirve:**  
Permite interceptar el envío para validar los datos antes de que el formulario navegue a otro lugar o envíe información al servidor.

**Importante:**

- Es común usar `event.preventDefault()` aquí para evitar el envío automático si algo no es válido.
    
- Solo se dispara en el `<form>`, no en los inputs individuales.
    

---

## **2. `reset`**

Se activa cuando el formulario es reseteado mediante:

- Un botón `type="reset"`
    
- La ejecución de `form.reset()`
    

**Qué hace:**  
Vuelve los valores de los campos a su estado inicial.

**Para qué sirve:**  
Para realizar acciones personalizadas cuando el usuario decide “borrar todo” del formulario.

---

## **3. `input`**

Se activa _cada vez que el valor de un campo cambia_, sin importar cómo:

- Teclado
    
- Pegar
    
- Borrar
    
- Autocompletado
    
- Cambios del sistema
    

**Se aplica a:**  
`<input>`, `<textarea>`, `<select>`.

**Para qué sirve:**  
Permite detectar modificaciones en tiempo real, útil para:

- Validación en vivo
    
- Contadores (ej.: “50/200 caracteres”)
    
- Actualización dinámica de la interfaz
    

---

## **4. `change`**

Se activa cuando un elemento cambia **y además pierde el foco**.  
Ejemplo: escribís en un input → mientras escribís NO se activa → salís del input → se activa.

**Se aplica a:**  
Todos los elementos que aceptan entrada: selectores, cajas de texto, checkbox, radio buttons, etc.

**Para qué sirve:**  
Para detectar cambios finales, no mientras el usuario está escribiendo. Es útil cuando no interesa cada carácter, sino el valor definitivo.

---

## **5. `focus` y `blur`**

Aunque pertenecen también a la categoría de “focus events”, se usan muchísimo en formularios, así que los incluimos acá porque afectan la interacción con inputs.

### `focus`

Se dispara cuando un campo recibe el foco (cuando se selecciona para escribir).

### `blur`

Se dispara cuando un campo pierde el foco.

**Para qué sirven:**

- Aplicar estilos cuando un usuario empieza a escribir
    
- Quitar mensajes de error cuando sale del campo
    
- Validar al dejar un input
    

---

## **6. `invalid`**

Se activa cuando un campo NO cumple una validación HTML5, por ejemplo:

- `required`
    
- `type="email"`
    
- `min`, `max`, `pattern`, etc.
    

**Importante:**

- Se dispara antes del envío
    
- Solo se activa en el campo que falló, no en el formulario
    
- No requiere JavaScript (HTML5 lo gestiona solo)
    

**Para qué sirve:**  
Permite personalizar el comportamiento cuando los datos no cumplen los requisitos.

---

## **7. `formdata`**

Un evento más moderno, que se dispara cuando se crea un objeto `FormData` a partir de un formulario (generalmente al enviar el form).

**Para qué sirve:**  
Permite modificar o inspeccionar los datos antes de enviarlos al servidor, sin necesidad de tocar directamente cada input.

---
