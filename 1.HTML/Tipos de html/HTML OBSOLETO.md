El **HTML obsoleto** se refiere a etiquetas o atributos de HTML que **ya no se recomiendan usar** porque han sido **reemplazados por mejores prácticas** o tecnologías más modernas, como **CSS para el diseño visual** y **HTML5** para una estructura más semántica.

### ¿Por qué es importante evitar HTML obsoleto?

1. **Compatibilidad futura**: Los navegadores podrían dejar de soportarlo.
    
2. **Accesibilidad**: El HTML moderno mejora la comprensión del contenido por lectores de pantalla.
    
3. **Separación de contenido y presentación**: HTML actual estructura el contenido; el diseño lo maneja CSS.

---

### **ETIQUETAS HTML OBSOLETAS**

|Etiqueta obsoleta|Uso original|Alternativa moderna|
|---|---|---|
|`<font>`|Cambiar tipo, tamaño y color de fuente|CSS: `font-family`, `font-size`, `color`|
|`<center>`|Centrar contenido|CSS: `text-align: center`|
|`<b>`|Texto en negrita|`<strong>` (si tiene énfasis semántico) o `font-weight` en CSS|
|`<i>`|Texto en cursiva|`<em>` (si tiene énfasis semántico) o `font-style` en CSS|
|`<u>`|Texto subrayado|CSS: `text-decoration: underline`|
|`<strike>`|Texto tachado|CSS: `text-decoration: line-through`|
|`<big>` / `<small>`|Aumentar o reducir tamaño|CSS: `font-size`|
|`<tt>`|Texto monoespaciado|CSS: `font-family: monospace`|
|`<s>`|Marcar texto como no válido|CSS: `text-decoration: line-through` o `<del>` (semántico)|
|`<blink>`|Hacer parpadear texto (Netscape)|¡Evítalo! Efectos similares con animaciones CSS (aunque poco recomendable)|
|`<marquee>`|Texto en movimiento (IE)|CSS `animation` (aunque se desaconseja por accesibilidad)|
|`<basefont>`|Establecer fuente base para todo el documento|CSS en `body` o global|

---

###  **ATRIBUTOS HTML OBSOLETOS**

|Atributo obsoleto|Se usaba en...|Alternativa moderna|
|---|---|---|
|`bgcolor`|`<body>`, `<table>`, `<td>`, etc.|CSS: `background-color`|
|`align`|Muchas etiquetas (`<div>`, `<img>`, etc.)|CSS: `text-align`, `margin`, `float`|
|`border`|`<img>`, `<table>`, etc.|CSS: `border`|
|`valign`, `halign`|En tablas (`<td>`, `<tr>`)|CSS: `vertical-align`, `text-align`|
|`width`, `height`|En imágenes, tablas, etc.|CSS: `width`, `height`|
|`name` en `<a>`|Anclas internas|Usa `id`|
|`nowrap`|Evitar que el texto se divida en varias líneas|CSS: `white-space: nowrap`|

---

### ¿Por qué no usarlos?

- No separan **contenido** de **presentación**.
    
- No son **semánticos**: el navegador no entiende el propósito del contenido.
    
- Muchos **no son compatibles** con HTML5.
    
- Dificultan el mantenimiento del código y el diseño adaptable (responsive).