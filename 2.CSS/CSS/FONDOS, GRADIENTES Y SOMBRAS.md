En esta sección vamos a definir y a ver como usar las propiedades que se utilizan en los fondos.
Para empezar tenemos la propiedad "background" y esta tiene muchas funciones dependiendo del valor a definir que le agreguemos.

#### **background-color**:
es una propiedad que nos permite cambiar el fondo del elemento o la caja en la que se encuentra, usando propiedades de colores ya vista anteriormente.

**background-image: url ("enlace")**: esta propiedad nos deja ponerle un fondo a la caja con un enlace url o enlace de la imagen.

**background-size**: esta propiedad hace que la imagen usado de fondo se ajuste o adapte a lo ancho  total de la caja. Esta propiedad se puede medir con estos valores,
**contain**: esto obliga al navegador a que la imagen se adaptarse en el espacio que le dimos y que  se vea al menos una vez. Sin no nos gusta que la imagen se repita, lo relacionamos con la la propiedad:
**background-repeat**: no-repeat. Aca podemos hacer que se repitan por ejes "**y**" o "**x**"
**cover**: hace que la imagen se adapte o se ajuste a la resolución que necesita tener. esto se puede complementar o ajustar con:
**background-position**: **right-center-left-top-bottom**: que mueve la imagen a de izquierda a derecha u centro o arriba y abajo. También se le puede dar coordenadas especificas  con unidades de medidas px.

**background-attachment:** **fixed**:  si queremos que la imagen usada de fondo se mueva con el scroll. para lograr el efecto la caja que lo contenga al fondo debe tener el margin 0. se puede definir esta propiedad con el valor **scroll o fixed** o l**ocal** que es para que la imagen no se salga del contenedor que funciona igual que scroll.

Para definir el fondo en un resumen directo podemos hacerlo asi:
background: url(enlace) top / cover fixed #f60000 
 de esta forma nos ahorramos el trabajo de definir de uno en uno.

## GRADIENTES

Es una ==transición suave de un color a otro o de varios colores en una imagen==. Es una forma de crear efectos visuales llamativos y dinámicos en elementos como fondos, botones, texto y más. Se puede utilizar en diferentes formas, como gradientes lineales (transiciones en línea recta) o radiales (transiciones circulares o elípticas).

 ![[images.jpg]]

En este caso para usar **linear**, debemos entender que **linear -gradient** es una funcion que se usa dentro de la propiedad **background**; Ej:

**Background: linear-gradient ( )**; nos pide que agreguemos un parámetro dentro de el. Que claramente seria dos colores a definir, ej: **Background: linear-gradient (red, black )**, podemos usar hasta un color de mas o usar el transparente y medirlo en porcentaje. Si queremos posicionar de donde queremos la sombra lo hacemos asi: **Background: linear-gradient (to right, red, black )**, puede ser right, left, top, button.

Como mencionamos anteriormente tenemos también a radial, es una especie de viñeta, esto hace que los colores se se muevan a partir de un radio. ej:
**Background: radial-gradient (red, black )**

También tenemos a conic que hace un efecto como si fuese un cono; ej
**Background: conic-gradient ( transparente, black)**
## SOMBRAS

Las sombras agregan profundidad realismos a los elementos, tenemos la sombra que le da a una caja o la sombra que le da a un texto o la sombra que le da aun elemento que por ahora le vamos a llamar elemento x.

Acá veremos como usar la propiedad **box-shadow** y sus parámetros , el primer parámetro nos pide que indiquemos cuanto pixeles nos movemos horizontalmente osea a la derecha o a la izquierda, el segundo cuanto se mueve hacia abajo, el tercero nos pregunta cuanto va a ser el difuminado y después pregunta cuanto queremos que la sombra se expanda y finalizado nos pedirá el color. ej;
**box-shadow: 0 0 40px 0 black**

En los textos usamos la propiedad Text-shadow, esta propiedad nos pide los mismos parámetros exceptuando la expansión ej:

**text-shadow: 0 0 3px red**

Por ultimo tenemos la propiedad que sirve para ponerle a imágenes transparentes o que tengan un canal Alpha que tenga png. para ello usamos la propiedad **filter** y dentro el parámetro **drop-shadow** y le damos los valores que conocemos, ejemplo:
**filter:drop-shadow** **(0 0 15px black)**.


