La **accesibilidad web** se refiere a que los **sitios web sean utilizables por todas las personas**, incluidas aquellas con **discapacidades físicas, visuales, auditivas, cognitivas o neurológicas**. Es una parte fundamental del diseño y desarrollo web moderno.
###  ¿Por qué es importante?

1. **Derechos de acceso**: Todos tienen derecho a usar la web.
    
2. **Inclusión**: Mejora la experiencia para personas con discapacidad.
    
3. **Legalidad**: En muchos países es obligatorio por ley (ej. Ley 26.653 en Argentina, ADA en EE.UU.).
    
4. **Mejor SEO y usabilidad**: Los sitios accesibles también benefician a usuarios sin discapacidades (por ejemplo, personas en lugares con mala conexión o usando el celular).
    

---

###  Principios de la Accesibilidad (POUR)

|Principio|Qué significa|
|---|---|
|**Perceptible**|La información debe ser detectable (texto alternativo, subtítulos, colores con buen contraste).|
|**Operable**|Se puede navegar con teclado, mouse u otros dispositivos.|
|**Comprensible**|El contenido debe ser fácil de entender, claro y consistente.|
|**Robusto**|Funciona bien en distintos dispositivos, navegadores y tecnologías asistivas (como lectores de pantalla).|

---

###  Buenas prácticas clave

|Práctica|Ejemplo|
|---|---|
|**Texto alternativo (alt)** en imágenes|`<img src="logo.png" alt="Logo de la empresa">`|
|**Usar etiquetas semánticas**|`<nav>`, `<main>`, `<footer>` ayudan a lectores de pantalla|
|**Buen contraste de colores**|Evitar texto gris claro sobre fondo blanco|
|**Navegación por teclado**|Todo debe ser accesible con `Tab`, sin necesidad de mouse|
|**Formularios accesibles**|Cada `<input>` debe tener un `<label>` claro|
|**Subtítulos y transcripciones**|Para videos y audios|
|**Evitar parpadeos**|Porque pueden causar convulsiones o malestar|
|**Evitar usar solo colores para comunicar**|Por ejemplo: "campos en rojo son obligatorios" → mejor también con texto o íconos|

---

###  Ejemplo de accesibilidad aplicada


`<form>   <label for="email">Correo electrónico:</label>   <input type="email" id="email" name="email" required> </form>`

Esto es mejor que simplemente:

`<input type="email" placeholder="Correo electrónico">`

Porque los lectores de pantalla **no pueden interpretar bien solo el placeholder**.

---

###  Herramientas útiles

- **WAVE** (WebAIM): https://wave.webaim.org/
    
- **Lighthouse** (en Chrome DevTools)
    
- **axe Accessibility Checker**
    
- **NVDA o VoiceOver**: Lectores de pantalla para probar accesibilidad real