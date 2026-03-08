## ¿Qué es la propiedad `position` en CSS?

La propiedad `position` define **cómo se posiciona un elemento en el documento**. Sus valores principales son:

- `static` (valor por defecto)
    
- `relative`
    
- `absolute`
    
- `fixed`
    
- `sticky`
    

 Nos vamos a enfocar en los dos más usados juntos:

### 🔹 `relative`

### 🔹 `absolute`

---

##  `Position: relative`

Esta propiedad **posiciona el elemento en relación a su posición original** (la que tendría si no tuviera `position: relative`).

### ✅ Características:

- El elemento **sigue ocupando su espacio original en el flujo del documento**.
    
- Puedes moverlo con las propiedades `top`, `right`, `bottom`, `left`.
    
- Otros elementos **no se "recolocan"** aunque el elemento se haya movido visualmente

Ya sabemos que para mover los elementos de lado a lado usamos las propiedades de (top, right, bottom, left), pero si tenemos un elemento que queremos sobreponerlo sobre otro, lo hacemos moviéndonos en el eje z, para ello usamos lo siguiente
## `z-index`

La propiedad `z-index` **no mueve un elemento físicamente en el eje Z**, pero **controla su orden de apilamiento visual**: qué elemento se muestra **encima** o **debajo** de otro.

## ¿Cómo funciona `z-index`?

- Cuanto **mayor el valor del `z-index`**, más **"encima"** se muestra el elemento.
    
- Los elementos con **z-index más bajo** se ven **debajo** de los de mayor valor.
    
- El valor puede ser positivo o negativo (`z-index: -1` también es válido).



## `Position: absolute`

Esta propiedad **saca al elemento del flujo del documento**, y lo **posiciona respecto al elemento contenedor más cercano que tenga `position: relative`, `absolute`, `fixed` o `sticky`**. Si no hay ninguno, se posiciona respecto al `body`.

### ✅ Características:

- **No ocupa espacio** en el diseño normal del documento.
    
- Se posiciona exactamente en las coordenadas `top`, `right`, `bottom`, `left` **del contenedor posicionado**.
    
- Muy útil para overlays, menús flotantes, modales, tooltips, etc.


## Diferencia clave entre `relative` y `absolute`

| Aspecto                                        | `relative`                 | `absolute`                                |
| ---------------------------------------------- | -------------------------- | ----------------------------------------- |
| ¿Ocupa espacio en el documento?                | Sí                         |  No                                       |
| ¿A qué se posiciona relativo?                  | A su **posición original** | Al **contenedor posicionado más cercano** |
| ¿Puede afectar la posición de otros elementos? | No directamente            | Sí, al estar fuera del flujo              |
| ¿Útil para...?                                 | Ajustes finos              | Superposiciones, tooltips, modales        |

# `Position: fixed`

### 

Un elemento con `position: fixed` **se queda fijado en un lugar específico** de la pantalla, **independientemente del scroll**. Siempre está visible, como una barra de navegación que no desaparece.

###  Características:

- Se posiciona **respecto al viewport** (la ventana del navegador).
    
- **No se mueve al hacer scroll.**
    
- No ocupa espacio en el flujo del documento (es como si estuviera flotando).
    
- Puedes usar `top`, `right`, `bottom`, `left` para ubicarlo.
    

---

## 📌 `position: sticky`

###  ¿Qué es?

Un elemento con `position: sticky` **actúa como `relative` normalmente, pero se "pega" al viewport** cuando llegas a una posición definida al hacer scroll. Muy útil para encabezados de tabla o menús de sección.

###  Características:

- Se posiciona **respecto al contenedor padre**.
    
- Se **"pega" al viewport solo después de un punto de scroll**.
    
- Vuelve a su flujo normal si el contenedor termina.

---

##  Diferencias clave

|Característica|`fixed`|`sticky`|
|---|---|---|
|Se posiciona respecto|Al viewport|A su contenedor padre|
|Se queda visible|Siempre, aunque scrollees mucho|Solo mientras el contenedor lo permita|
|Ocupa espacio|No|Sí (hasta que se fija)|
|Uso típico|Menús fijos, botones flotantes|Encabezados, navegación de sección|
