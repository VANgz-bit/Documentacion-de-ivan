En esta sección vamos a encontrar 3 formas para definir o crear colores, el primero es:  

### RGB(red, green, blue).

Primero tenemos que entender que hay 256 combinaciones para cada color, osea que hay 256 tipos de rojos y de azul y de verde, de tal forma si multiplicamos 256 por 256 por 256 que nos  da una cantidad de 16.777.216 combinaciones posibles de colores, tenemos también al Alpha que es un canal aparte que define la transparencia de cada color creado. Entonces ya aclarado lo anterior.
Si queremos crear un color debemos seleccionar una combinación especifica ej
![[Pasted image 20250424224846.png]]
RED tiene 256 tipos de rojo osea que tenemos que seleccionar un nro del 0 al 255, lo mismo aplica para azul y verde, elegimos la cantidad que queremos mezclar o agregar de cada color.

.box{
 background-color: rgb(255,0,255)
}

Acá como podemos ver ,cree el color violeta puse el máximo de rojo y el máximo de azul. Hay miles de combinaciones posibles , si queremos el gris, ponemos la misma cantidad de pintura y nos da el color deseado. Cabe aclarar que mientras mas cerca del 0 estamos mas oscuro será nuestro color y mientras mas cerca del 255 mas claro será.

### COLORES HEXADECIMALES

En este sistema de 16 tonos por color en donde cada color tiene otros 16 tonos de colores, el sistema esta medido del 1 al 16, pero para los colores es del 0 al 9 y del 10 al 6 lo continuamos con letras del A al F, de tal forma que quedaría asi 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F.
 si queremos crear un color seria asi #ff0000 asi creariamos rojo
si queremos un violeta seria #ff00ff.

como dijimos mientras mas subimos al máximo tono mas se usa del color, f es el maximo y el maximo de f es f, es decir que cada primer tono definido tiene otro tono, es decir, que si yo aplico f siendo este el maximo de rojo le puedo poner otro tono de rojo usando la misma escala, si quiero un tono de rojo distino voy a hacer #f60000

![[Pasted image 20250426090927.png]]

En esta imagen tenemos ejemplificado como se definen algunos colores con el sistema rgb y el sistema hexadecimal.

### HSL (HUE, SATURATION, LIGHTNEES)

Este sistema es una rueda de colores como su abreviatura lo dice (hue), donde este valor se mide por grados, y la saturación y el brillo se miden por porcentajes. ej

![[149501735.jpg]]

De esta forma si queremos rojo vamos a poner hsl (0, 100%, 50%).

