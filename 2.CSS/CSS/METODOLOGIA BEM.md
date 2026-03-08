
### ¿Qué es BEM?

**BEM** significa **Block - Element - Modifier (Bloque - Elemento - Modificador)**.  
Es una convención de nombres para clases CSS que ayuda a escribir código más organizado y predecible, especialmente en proyectos grandes o con varios desarrolladores.

---

### ¿Por qué usar BEM?

- **Claridad:** Se entiende fácilmente la estructura del HTML/CSS.
    
- **Reutilización:** Facilita reutilizar componentes sin conflictos de estilos.
    
- **Escalabilidad:** Soporta grandes bases de código sin volverse caótico.
    
- **Evita conflictos:** Minimiza los errores por nombres de clases globales.
    

---

### Estructura BEM

#### 1. **Bloque (`Block`)**

Es la unidad independiente de la interfaz: un botón, un menú, un formulario, una tarjeta, etc.

- Representa **un componente autónomo**.
    
- Nombre: `bloque`

html

`<div class="boton">Enviar</div>`

#### 2. **Elemento (`Element`)**

Es una parte del bloque que **no tiene sentido por sí sola** y depende del bloque (por ejemplo, el ícono dentro del botón).

- Se nombra con doble guion bajo: `bloque__elemento`
`<div class="boton">`
  `<span class="boton__icono">🚀</span>`
  `<span class="boton__texto">Enviar</span>`
`</div>`
`
#### 3. **Modificador (`Modifier`)**

Es una **variación o estado** del bloque o del elemento (por ejemplo, botón grande, botón deshabilitado, color diferente).

- Se nombra con doble guion medio: `bloque--modificador` o `bloque__elemento--modificador`

`<div class="boton boton--grande boton--primario">`
  `<span class="boton__icono boton__icono--blanco">🚀</span>`
  `<span class="boton__texto">Enviar</span>`
`</div>`

