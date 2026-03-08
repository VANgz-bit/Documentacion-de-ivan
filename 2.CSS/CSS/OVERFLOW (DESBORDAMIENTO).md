La propiedad `overflow` controla qué sucede con el **contenido que no cabe** dentro de su contenedor.

ejemplo:

selector {
  overflow: visible | hidden | scroll | auto;
}

## Valores posibles de `overflow`

| Valor                   | Descripción                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| `visible` (por defecto) | El contenido que se desborda **se muestra igual** fuera del contenedor.                             |
| `hidden`                | El contenido extra **se recorta y no es visible**.                                                  |
| `scroll`                | Siempre aparecen barras de desplazamiento (horizontal y/o vertical), **aunque no sean necesarias**. |
| `auto`                  | Solo aparece la **barra de desplazamiento si es necesaria** (cuando el contenido se desborda).      |


## También se puede usar `overflow-x` y `overflow-y`

Estas propiedades controlan el overflow **horizontal y vertical por separado**.

overflow-x: hidden;
overflow-y: auto;   /* Muestra scroll vertical si es necesario */


# CONTROL DE FLUJO DE TEXTOS

## ¿Qué es el control de flujo de texto en CSS?

Es el conjunto de propiedades que te permiten manejar cómo **fluye**, **se ajusta**, **se corta**, o **se muestra el texto** dentro de un elemento HTML, especialmente cuando el texto **es más largo que el contenedor** o necesita un formato específico.

---

##  Propiedades clave para controlar el flujo de texto

### 1. **`white-space`**

Controla cómo se manejan los **espacios en blanco** y los **saltos de línea** en el texto.

|Valor|Comportamiento|
|---|---|
|`normal`|El texto se ajusta automáticamente, colapsa espacios en blanco, y se ajusta a múltiples líneas.|
|`nowrap`|Todo el texto se mantiene en **una sola línea** (aunque se desborde).|
|`pre`|Se respeta **exactamente** el espaciado y los saltos de línea (como en `<pre>`).|
|`pre-wrap`|Respeta saltos de línea manuales y permite que el texto se ajuste.|
|`pre-line`|Colapsa espacios pero respeta saltos de línea.|

#### Ejemplo:

`.texto {
white-space: nowrap;
}`

---

### 2. **`overflow` + `text-overflow` + `white-space` (para textos largos)**

Esta combinación es muy usada para cortar texto en una sola línea con puntos suspensivos.

.texto-cortado {
  white-space: nowrap;        /* No saltos de línea */
  overflow: hidden;           /* Oculta el texto que desborda */
  text-overflow: ellipsis;    /* Muestra "..." al final */
}

✅ Muy útil para títulos o tarjetas con espacio limitado.

---

### 3. **`word-wrap` (ahora `overflow-wrap`)**

Permite que las palabras largas (como URLs) se **dividan para evitar desbordes**.

texto {
  overflow-wrap: break-word; /* También puede usarse word-wrap: break-word; */
}

---

### 4. **`word-break`**

Controla cómo se rompen las palabras si no caben en su contenedor.

|Valor|Significado|
|---|---|
|`normal`|Solo se rompe en espacios o guiones.|
|`break-word`|Rompe las palabras largas si es necesario.|
|`break-all`|Puede romper palabras en **cualquier carácter**.|
|`keep-all`|Evita que las palabras se rompan (útil en idiomas como el japonés o chino).|

#### Ejemplo:


`.texto {
	word-break: break-word;
}`

---

### 5. **`direction` y `unicode-bidi`** (para control de texto bidireccional)

- `direction: ltr;` – texto de izquierda a derecha (por defecto)
    
- `direction: rtl;` – texto de derecha a izquierda (como árabe o hebreo)
    

`unicode-bidi` te da control avanzado para manejar mezclas de idiomas.