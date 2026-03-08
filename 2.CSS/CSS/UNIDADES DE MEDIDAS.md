En este apartado tenemos dos clases de medidas "ABSOLUTAS Y RELATIVAS"
Las medidas absolutas definen un valor fijo y no cambian en función de otros factores, mientras que las medidas relativas dependen de un valor de referencia y pueden variar.

Las clases de medidas que solemos usar en absolutas son:
px(pixeles), cm(centímetros), mm(milímetros), in (pulgadas).
Cuando trabajamos con medidas reales que sirven para medir cosas en la vida reales como banners o impresiones usamos las medidas como mencionamos anteriormente exceptuando los pixeles. En otras palabas son medidas físicas. Entonces las medidas físicas son ideales para tener control y ser específicos.

las clases de medidas que se usa en las relativas son:

- **Porcentajes (%)**: Se refieren al ancho o alto del elemento padre. 

- `em`: Se refiere al tamaño de la fuente del elemento padre, osea que tomamos la medida de elemento padre y la multiplicamos por cuantas veces queramos. si el elemento padre mide 5 px y quiero que mi em mida 25 tendríamos un em de valor 5(5em) porque 5 veces 5 es igual a 25.

- `rem`: Se refiere al tamaño de la fuente del elemento raíz (por lo general, `<html>`). Si el elemento raíz no esta definido este automáticamente buscara etiqueta por etiqueta hasta encontrar el elemento raíz y en caso de no hacerlo esta se pondrá en en valor predeterminado 16px.

- `ex`: Se refiere a la altura de la letra "x" de la fuente del elemento. 

- `ch`: Se refiere al ancho de la letra "0" de la fuente del elemento. 

- `vh`: Se refiere al 1% del alto de la ventana gráfica. 

- `vw`: Se refiere al 1% del ancho de la ventana gráfica. 

- `vmax`: Se refiere al 1% del mayor valor entre el ancho y el alto de la ventana gráfica. 

- `vmin`: Se refiere al 1% del menor valor entre el ancho y el alto de la ventana gráfica.