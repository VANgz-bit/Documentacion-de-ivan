 ¿Qué es la herencia en CSS?

**La herencia en CSS** es el mecanismo por el cual **algunos estilos aplicados a un elemento padre se transfieren automáticamente a sus elementos hijos** (descendientes), sin que tengas que volver a escribir esos estilos.

Es muy parecido a cómo los hijos heredan características de los padres en la vida real. Sin embargo, en CSS **no todas las propiedades son heredables** por defecto.

---

 Propiedades que _sí_ se heredan por defecto

Solo **ciertas propiedades, usualmente relacionadas con el texto**, se heredan automáticamente. Ejemplos:

|Tipo|Propiedades que se heredan|
|---|---|
|Texto|`color`, `font-family`, `font-size`, `font-style`, `font-variant`, `font-weight`, `letter-spacing`, `line-height`, `text-align`, `text-indent`, `text-transform`, `visibility`, `white-space`, `word-spacing`, `direction`|
|Tablas|`border-collapse`, `caption-side`, `empty-cells`|
|Listas|`list-style`, `list-style-position`, `list-style-type`, `list-style-image`|
|Accesibilidad|`quotes`|

### Ejemplo:

`<div style="color: blue;">   <p>Este texto será azul</p> </div>`

👉 Aunque no le diste `color: blue` al `<p>`, lo **hereda** del `<div>`.

---

##  Propiedades que _no_ se heredan por defecto

Muchas propiedades **no se heredan automáticamente**, como:

- `margin`, `padding`, `border`
    
- `width`, `height`
    
- `background`, `display`, `position`, `float`
    
- `box-shadow`, `z-index`, etc.
    

Estas propiedades **deben declararse explícitamente** si deseas aplicarlas a los hijos.

---

##  ¿Cómo forzar la herencia?

Si deseas que una propiedad **no heredable** se herede, puedes usar el valor especial `inherit`:

`div {   background-color: blue; }  p {   background-color: inherit; /* Hereda el fondo azul del div */ }`

También existen otros valores clave útiles:

- `initial`: restaura al valor por defecto del navegador.
    
- `unset`: actúa como `inherit` para propiedades heredables y como `initial` para las no heredables.
    
- `revert`: revierte al valor definido por el usuario o el navegador (menos común).
    

---

##  Reglas importantes sobre la herencia

- **Es más eficiente** dejar que las propiedades se hereden cuando sea posible (menos código).
    
- **Los estilos en cascada y la especificidad** pueden sobrescribir los valores heredados.
    
- Puedes combinar herencia con `em` o `%` para tamaños relativos a padres


# ESPECIFIDAD Y CASCADA

## Qué es la **cascada** en CSS?

La palabra **CSS** significa _Cascading Style Sheets_ o _Hojas de Estilo en Cascada_.  
La **cascada** se refiere al **proceso que CSS usa para decidir qué reglas aplicar cuando hay múltiples reglas que afectan al mismo elemento**.

CSS combina todas las reglas aplicables, y luego decide **cuál tiene más peso** y se aplicará finalmente.

---

### ✅ ¿Cómo decide CSS qué regla aplicar?

CSS usa un sistema de prioridades basado en:

1. **Importancia (origen):**
    
    - Estilos del navegador (por defecto)
        
    - Estilos del usuario (por ejemplo, accesibilidad)
        
    - Estilos del autor (tu CSS)
        
    - Estilos con `!important` (los más fuertes, en teoría)
        
2. **Especificidad** (lo veremos abajo)
    
3. **Orden de aparición** (si todo lo demás es igual, gana la que aparece más abajo en el código)
    

---

## 🔶 ¿Qué es la **especificidad** en CSS?

La **especificidad** es una puntuación que CSS asigna a cada selector para saber **qué tan específico** es.  
Cuanto más específico, **más peso tiene** y más probabilidad de aplicar su estilo.

### 📊 Puntuación de especificidad:

CSS evalúa cada selector como un número de **cuatro niveles**: `a, b, c, d`:

|Tipo de selector|Valor específico|Ejemplo|Puntos|
|---|---|---|---|
|Inline style|`a`|`style="..."`|`1,0,0,0`|
|ID selector|`b`|`#header`|`0,1,0,0`|
|Clase, atributo, pseudo-clase|`c`|`.menu`, `[type="text"]`, `:hover`|`0,0,1,0`|
|Elemento, pseudo-elemento|`d`|`div`, `p`, `::after`|`0,0,0,1`|

> 🔸 _Entre más alto en la tabla, más poder tiene._  
> 🔸 _`!important` puede sobreescribir todo, incluso la especificidad, pero debe usarse con cuidado._

---

### 🧠 Ejemplo práctico:


`/* 0,0,0,1 → etiqueta */

p {  
	color: red; 
}

/* 0,0,1,0 → clase */ 

.texto {   
color: blue; 
}  

/* 0,1,0,0 → ID */
```
#importante {  
```
color: Green; 
}

/* HTML */ 

`<p class="texto" id="importante">Hola mundo</p>`

🟢 Resultado: **el texto será verde**, porque `#importante` (ID selector) tiene más especificidad.

---

### ⚠️ ¿Y si hay dos reglas con misma especificidad?

Entonces **gana la que aparece más abajo en el archivo CSS**.

---




