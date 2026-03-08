Antes para que una pagina pueda cargar un audio o video se usaba flash hasta se desarrollaba juegos con flash, actualmente ya no se usa flash por diversas maneras tal que html 5 creo dos etiquetas para no depender de lo mencionado, `<video> y <audio>.`

la etiqueta `<video>` tiene atributos que agregar

**SRC="/video/clip.mp4"** esta atributo sirve como ya sabemos para cargar la url de archivo o enlace que queremos que se cargue.

**Controls**: sirve para que el video tenga botones de interacción desde subirle el volumen o poder pausarlo.

Tenemos dos etiquetas que funcionan juntas, usamos **autoplay** para que el video se reproduzca automáticamente y **muted** para que se reproduzca sin sonido, el video no cargara sin estos dos atributos. En caso que el video no cargue correctamente usamos **`alt`** y ponemos una descripción de lo que debería haber. 

**Loop** nos sirve para que el video se reproduzca en bucle.

#### SUBTITULOS

También tenemos una etiqueta llamada <`track`> que se auto cierra sola, es una self close sintax, sirve para poner subtítulos a los videos, esta etiqueta no se puede editar en css se lo hace desde java script. Dentro de ella usamos el atributo **src** y dentro de el definimos "captions.vtt" y ahora si tenemos subtítulos, si queremos los subtítulos de otra manera lo podemos poner por **default**,
luego usamos otro atributo que es **kind** y definimos que es un **subtitle** o un **captions** que nos da una transcripción del audio o una traducción, también, otro es el **descriptions** que se usa para describir el video para personas ciegas, entre otros. 
Otro atributo importante es **srclang="es"** que le indicamos al navegador de que idioma es el subtitulo, y si queremos que el usuario elija la  region abrimos un l**abe**l en estilo atributo y le damos Español (Latinoamérica)

Cabe aclarar que para poner los subtitulos el campo de captions debe de estar enlazado con el archivo captions osea que vamos a tener que escribir manualmente.

Para los videos debemos asegurarnos de que si queremos el audio del video lo convirtamos en audio el video y facilitar que cargue bien , porque de lo contrario Google cargará primero el video y después el audio.

---
# OBJET FIX Y OBJET POSITIONS

Las propiedades **`object-fit`** y **`object-position`** en CSS son muy útiles para controlar cómo se muestran **imágenes**, **videos**, y otros medios embebidos dentro de un contenedor, **especialmente cuando sus proporciones no coinciden** con las del contenedor.


## 🖼️ ¿Qué es `object-fit`?

La propiedad `object-fit` define **cómo se ajusta el contenido de un elemento `<img>`, `<video>`, o `<iframe>` al tamaño de su contenedor**.

Es similar a cómo funciona `background-size` para imágenes de fondo, pero se aplica a elementos reales.

---

###  Sintaxis

`img {
object-fit: cover;
}`

---

###  Valores de `object-fit`

| Valor        | Comportamiento                                                                                                                   |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| `fill`       | (valor por defecto) Estira el contenido para que llene todo el contenedor. **Puede deformarlo**.                                 |
| `contain`    | Escala el contenido para que **quepa completamente**, manteniendo su proporción. **Puede dejar espacio vacío** (barras blancas). |
| `cover`      | Escala el contenido para **llenar todo el contenedor**, manteniendo proporciones. **Puede recortar el contenido**.               |
| `none`       | No escala. Muestra el contenido con su tamaño original. Puede salirse del contenedor.                                            |
| `scale-down` | Usa el menor tamaño entre `none` y `contain`. Si el contenido ya es más pequeño que el contenedor, **no se escala**.             |

 EJEMPLO PRACTICO:

EN HTML:

`<div class="contenedor">`
  `<img src="foto.jpg" class="imagen">`
`</div>`

EN CSS

.contenedor {
  width: 300px;
  height: 200px;
  overflow: hidden;
}

.imagen {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

Con `cover`, la imagen se recorta para llenar el contenedor sin deformarse.

## ¿Qué es `object-position`?

Esta propiedad **define la posición del contenido dentro del contenedor**, **cuando no llena completamente el área** (usualmente con `contain`, `none`, `scale-down`).

---

### ✅ Sintaxis

`img {
object-fit: contain;
object-position: center top;}
}`

---

###  Valores de `object-position`

- Puedes usar **palabras clave**: `center`, `top`, `left`, `right`, `bottom`.
    
- O valores porcentuales o de longitud: `50% 50%`, `10px 20px`.