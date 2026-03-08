Este mas que nada no es una propiedad sino mas bien un concepto de como se debe describir como se debería poner los elementos de html en una pagina web 
este modelo lo que hace es definir como esas cajas se dimensionan cambian su tamaño y como interactúan entre si

 
![[1_nmdxvJbL2GI5NQSXCLOskA.webp]]
El **Padding** o relleno es el espacio entre el contenido y el borde del elemento, este espacio aumenta el area alrededor del contenido dentro del elemento

El **Borde**r o borde es una linea que rodea tanto al contenido como el pading y se puede controlar el estilo el grosor y el color del borde

El **Margen** es el espacio que esta alrededor de la caj fuera del borde y este espacio separa otros elementos en la pagina a diferencia de los anteriores el margin no forma parte de la caja lo unico que hace es separar elementos de otras paginas.

También tenemos elementos como el **width y high**t que hacen que aumente o disminuya la altura y el grosor de la caja.
Cabe aclara que con el width podemos medirlo por el 100% en para que se adapte a cualquier dispositivo

Para trabajar con estas propiedades vamos a usar una etiqueta de bloque que sirve para divir nada mas 


### PADING Y MARGIN


Como ya dijimos antes el padding es el espacio entre el contenido y el borde del elemento.
Como ya aprendimos a seleccionar elementos con los selectores ahora podemos seleccionar en la hoja  de estilos y modificar el contenido en la caja 

cuando usamos el padding solemos usar el sistema de medicion de pixeles "px"
y al aplicar una vez este define todo el padding en lo medido ej

.formulario{
	background color: red
		padding 30px
}
Asi se definió que todo lo que esta alrededor del contenido mida 30 pixeles, si queremos definir cada lado por diferentes medidas aplicamos un método poco ortodoxo

.formulario{
	backgroundcolor : red
		padding-top 20px,
		padding-right 10px
		padding-bottom 30px
		padding-left 15 px
}
De esta forma nosotros adjuntamos distintitas mediciones pero aun asi no es recomendada, se suele usar de la siguiente forma,

.formularios{
		padding 20px 10px 30px 15px
}
Esta es la forma eficiente de usar la medición, para no confundirnos cual es cual nos solemos mover en dirección de las agujas del reloj, osea que arrancamos con padding-top en adelante.

La otra forma es que definimos el valor usado solo dos propiedades 
horizontal y vertical 

.formulario{
	padding 30px 50px
}

El primer valor que di corresponde desde arriba y abajo, osea que por arriba y por debajo del contenido solo va a medir 30px (top-bottom) y en cambio el segundo valor que definí corresponde a izquierda y derecha (left-right).

### BORDER (BORDE)

Ya dijimos que el border es una propiedad que remarca el padding y el contenido.
esta se puede cambiar sus aspectos fundamentales que se van a remarcar en estos ejemplos:

BORDER-WIDITH: esta propiedad cambia de tamaño el borde.
BORDER-STYLE: este cambia el estilo ya sea cambiar el borde con lineas con doble borde.
BORDER-COLOR: con esto podemos cambiar la propiedades del color del borde
BORDER-RADIUS: nos permite modificar las esquinas de un elemento

Hasta ahora entendemos que de esta forma podemos definir las cosas pero existe una propiedad que define esas tres propiedades anteriores en una sola que básicamente es lo mismo que vimos como padding.
Usamos la misma propiedad bolder y dentro de ella definimos lo que vimos anteriormente pero omitimos los clasificados de esta forma quedaría

.formulario{
		border : 3px solid black
}

El primero valor que vemos es el border-width el segundo es el border-style y el tercero border-color, asi de esta forma tendríamos resumido 3 valores en una sola.

Hay otras formas de definir bordes en el caso que queramos modificar o agregar en un área especifica el borde.
Si queremos un borde que solo se ponga a la derecha aplicamos:

border-right: 3px solid black;

Si queremos solo arriba: border-top: 3px solid black;


### BOX SIZING

 El box sizing es una propiedad de css que se utiliza para afectar el modelo de caja predeterminado, el modelo de caja es como los navegadores calculan el total de tamaño de un elemento.
 Calculamos el total tamaño de un elemento, para ello imaginamos las partes de una caja el contenido, el padding, etc.
 Lo primero que tenemos en cuenta es que el contenido mide 100px de width y 100px de height, esto esta definido que la caja tiene 100px, ´pero al agregar el padding y otros elementos su tamaño aumenta.
 Una de las formas que surgió fue medir a partir de border, entonces de esta forma le decimos al navegador que el tamaño que le damos para la caja incluye (contenido, padding, borde) dejamos de lado el margen, esto equivaldría a tener una caja de tamaño fijo, es decir que la caja va a medir 100px  sin importar cuanto padding o border le pongamos no va a cambiar su valor, todo lo que entre dentro de esta caja se va a ajustar al valor predispuesto fijo.

Para hacer el calculo automatico y que las poriedades se adapten al valor que queramos indicar usamos la propiedad box-sizing: border-box
ejemplo:

Si hacemos una caja y queremos que a lo largo y ancho mida 100px usamos la propiedades que ya vimos

width: 100px
height:100px

el contenido mide a lo largo y ancho 100px pero si agrego un padding de 10px
ahora mide 110px, y si agregamos un margin de 3 px ahora mide 113px y si agregamos un border de 10px nos queda en total de 123px, entonces con la propiedad BOX-SIZING: BORDER-BOX le decimos que adapte desde el contenido hasta el borde omitiendo el margen.
Asi de esta forma el navegador calcula cuanto valor debe tener cada propiedad para que el total de un resultado de 100px x 100px

.box{
	box-sizign: border-box;
	width: 100px;
	height: 100px;
	border: 10px solid black;
	padding: 5px;
	margin: 30px;
}

De esta forma los valores de padding, content, border se ajustan a un valor que como resultado dee 100px de ancho y de largo.



# **OUTLINE (CONTORNO)**


## ¿Qué es `outline`?

`outline` es una **línea que se dibuja alrededor de un elemento** para destacarlo, **sin afectar el tamaño o el flujo del layout**.

 **Diferencia clave con `border`**:

- `border` **ocupa espacio** en el diseño.
    
- `outline` **no ocupa espacio adicional**; se dibuja por fuera del borde.
    

---

##  ¿Para qué se usa?

- **Accesibilidad y navegación por teclado** (por ejemplo, al hacer `tab` en un formulario).
    
- **Resaltar elementos activos o enfocados**.
    
- **Depuración de diseño** (como una guía visual no destructiva).
    
- **Estilizar elementos interactivos** sin alterar el diseño.
    

---

##  Sintaxis de `outline`

`selector {
outline: `<width> <style> <color>`;
}`

Todos los valores son **opcionales** pero si usas uno solo, suele ser el color.

###  Ejemplo:

`button {
outline: 2px dashed red;
}`


##  Propiedades relacionadas

Además del shorthand `outline`, puedes usar las siguientes propiedades individualmente:

|Propiedad|Función|
|---|---|
|`outline-color`|Color del contorno.|
|`outline-style`|Tipo de línea: `solid`, `dashed`, `dotted`, `double`, etc.|
|`outline-width`|Grosor de la línea: `thin`, `medium`, `thick`, o valores en `px`, `em`, etc.|
|`outline-offset`|**Separación entre el borde del elemento y el contorno**.|

---

###  Ejemplo completo:

`input:focus { 
outline-color: blue
;   outline-style: solid;
outline-width: 3px;
outline-offset: 5px; }`

Esto aplica un contorno azul sólido de 3px de grosor, separado 5px del borde, **cuando el input tiene el foco**.

---

##  `outline` vs `border`

|Característica|`outline`|`border`|
|---|---|---|
|Afecta el layout|❌ No|✅ Sí|
|Se puede separar|✅ Con `outline-offset`|✅ Con `margin`/`padding`|
|Compatible con foco|✅ Sí (muy usado en focus)|🔄 Menos común|
|Se puede redondear|❌ No sigue `border-radius`|✅ Sí|
|Se puede animar|⚠️ Limitado|✅ Sí con `transition`|

---

##  Accesibilidad y `outline`

Algunos desarrolladores **quitan el `outline` en elementos `:focus` para “mejorar la estética”**, pero **esto rompe la accesibilidad** para usuarios que usan el teclado. Si decides quitarlo, asegúrate de **sustituirlo por otro indicador claro**.

###  Malo:


`button:focus {
outline: none;
}`
###  Mejor:


`button:focus {
outline: none;
box-shadow: 0 0 0 3px #3b82f6;
}`

---

##  `outline-offset`: separación visual

`input:focus {
outline: 2px solid blue;
outline-offset: 4px;
}`

Esto separa visualmente el contorno, útil para crear efectos más estéticos sin interferir con el diseño interno.

---

##  Uso práctico y depuración

Una técnica común de depuración es usar `outline` para ver los elementos en pantalla:

`* {
outline: 1px solid red;
}`

Esto dibuja un contorno rojo en cada elemento, sin modificar el diseño. ¡Perfecto para detectar alineaciones o márgenes inesperados!

















