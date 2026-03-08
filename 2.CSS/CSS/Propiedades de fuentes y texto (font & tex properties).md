
##  1. PROPIEDADES DE TEXTO

Estas propiedades afectan cómo se ve y se comporta el **contenido textual**, sin alterar la fuente directamente.

### 🔸 `color`

- Define el color del texto.
    
- Ejemplo:
    
    ```css
    color: red;        /* palabra clave */
    color: #ff0000;    /* hexadecimal */
    color: rgb(255,0,0); /* RGB */
    ```
    

---

### 🔸 `text-align`

- Alinea el texto dentro de su contenedor.
    
- Valores:
    
    - `left`: a la izquierda (por defecto en idiomas latinos)
        
    - `right`: a la derecha
        
    - `center`: centrado
        
    - `justify`: alinea ambos extremos agregando espacios entre palabras
        
- Ejemplo:
    
    ```css
    text-align: justify;
    ```
    

---

### 🔸 `text-decoration`

- Añade decoraciones como subrayado o tachado.
    
- Valores:
    
    - `none`: sin decoración
        
    - `underline`: subrayado
        
    - `line-through`: tachado
        
    - `overline`: línea arriba
        
- Ejemplo:
    
    ```css
    text-decoration: underline;
    ```
    

---

### 🔸 `text-transform`

- Cambia el formato del texto.
    
- Valores:
    
    - `none`: sin transformación
        
    - `uppercase`: todo en mayúsculas
        
    - `lowercase`: todo en minúsculas
        
    - `capitalize`: la primera letra de cada palabra en mayúscula
        
- Ejemplo:
    
    ```css
    text-transform: capitalize;
    ```
    

---

### 🔸 `text-indent`

- Agrega sangría en la primera línea de un párrafo.
    
- Se puede usar con `px`, `em`, `%`, etc.
    
- Ejemplo:
    
    ```css
    text-indent: 30px;
    ```
    

---

### 🔸 `letter-spacing`

- Espaciado entre letras.
    
- Valor por defecto: `normal`
    
- Ejemplo:
    
    ```css
    letter-spacing: 2px;
    ```
    

---

### 🔸 `word-spacing`

- Espaciado entre palabras.
    
- Valor por defecto: `normal`
    
- Ejemplo:
    
    ```css
    word-spacing: 1em;
    ```
    

---

### 🔸 `line-height`

- Altura de línea (distancia vertical entre líneas).
    
- Acepta valores como `normal`, número (`1.5`), unidades (`20px`) o porcentaje (`150%`).
    
- Muy importante para la legibilidad del texto.
    
- Ejemplo:
    
    ```css
    line-height: 1.6;
    ```
    

---

### 🔸 `white-space`

- Controla cómo se maneja el espacio en blanco.
    
- Valores clave:
    
    - `normal`: colapsa espacios y permite saltos de línea automáticos (por defecto)
        
    - `nowrap`: evita los saltos de línea
        
    - `pre`: conserva espacios y saltos como en un archivo `.txt`
        
    - `pre-line`, `pre-wrap`: combinaciones intermedias
        
- Ejemplo:
    
    ```css
    white-space: nowrap;
    ```
    

---

### 🔸 `direction`

- Define la dirección del texto:
    
    - `ltr`: de izquierda a derecha
        
    - `rtl`: de derecha a izquierda (idiomas como árabe o hebreo)
        
- Ejemplo:
    
    ```css
    direction: rtl;
    ```
    

---

### 🔸 `text-overflow`

- Controla qué ocurre cuando el texto se desborda.
    
- Requiere:
    
    ```css
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    ```
    
- Valor más usado: `ellipsis` (agrega "...")
    
- Ejemplo:
    
    ```css
    text-overflow: ellipsis;
    ```
    

---

### 🔸 `word-break` y `overflow-wrap`

- Controlan cómo se parte el texto cuando no cabe:
    
    - `word-break: break-word;`
        
    - `overflow-wrap: break-word;`
        
- Útiles para evitar desbordes en palabras largas.
    

---

##  2. PROPIEDADES DE FUENTE

Estas propiedades afectan el **tipo, tamaño y estilo** de la fuente.

### 🔸 `font-family`

- Define el tipo de letra.
    
- Se sugiere escribir primero fuentes específicas, luego genéricas como `sans-serif`, `serif`, `monospace`.
    
- Se pueden agrupar varias separadas por coma.
    
- Ejemplo:
    
    ```css
    font-family: 'Roboto', Arial, sans-serif;
    ```
    

---

### 🔸 `font-size`

- Tamaño de la fuente.
    
- Acepta unidades como `px`, `em`, `rem`, `%`, `vw`, etc.
    
- Ejemplo:
    
    ```css
    font-size: 16px;
    font-size: 1.2em;
    ```
    

---

### 🔸 `font-weight`

- Grosor del texto.
    
- Valores comunes:
    
    - `normal` (400), `bold` (700)
        
    - Números: 100 (más fino) a 900 (más grueso)
        
- Ejemplo:
    
    ```css
    font-weight: bold;
    font-weight: 300;
    ```
    

---

### 🔸 `font-style`

- Estilo de la fuente.
    
- Valores:
    
    - `normal`
        
    - `italic`: cursiva real
        
    - `oblique`: inclinación simulada
        
- Ejemplo:
    
    ```css
    font-style: italic;
    ```
    

---

### 🔸 `font-variant`

- Controla efectos tipográficos, como versalitas.
    
- Valor común:
    
    - `small-caps`: transforma minúsculas a mayúsculas pequeñas.
        
- Ejemplo:
    
    ```css
    font-variant: small-caps;
    ```
    

---

### 🔸 `font`

- Propiedad abreviada para varias propiedades de fuente.
    
- Orden:
    
    ```css
    font: font-style font-variant font-weight font-size/line-height font-family;
    ```
    
- Ejemplo:
    
    ```css
    font: italic small-caps bold 16px/1.5 'Georgia', serif;
    ```
    

---

### 🔸 `@font-face`

- Permite cargar fuentes personalizadas.
    
- Ejemplo:
    
    ```css
    @font-face {
      font-family: 'MiFuente';
      src: url('miFuente.woff2') format('woff2');
    }
    
    p {
      font-family: 'MiFuente';
    }
    ```
