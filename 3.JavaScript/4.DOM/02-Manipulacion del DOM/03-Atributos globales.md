## 🌍 ¿Qué son exactamente los atributos globales?

Los **atributos globales** son aquellos que **pueden aplicarse a cualquier elemento HTML**, sin importar su tipo (ya sea `<div>`, `<p>`, `<input>`, `<section>`, `<button>`, etc.).  
Se llaman _globales_ porque son parte del **modelo de contenido universal del HTML Living Standard (WHATWG)** y están **definidos para todos los elementos** del DOM.

Sin embargo, no todos son igual de útiles desde JavaScript: algunos influyen en **accesibilidad, idioma o comportamiento del navegador**, mientras que otros sirven para **identificación, datos o estilos**, que son los que manipulamos más comúnmente en el DOM.

---

## 🧩 Clasificación y desarrollo de los principales grupos de atributos globales

En lugar de listarlos superficialmente, los agrupemos según su **función real dentro del DOM** y expliquemos cómo se comportan.

---

### 1️⃣ Atributos de **identificación y relación con el DOM**

Estos definen la identidad o conexión del elemento dentro del árbol del DOM.

- **`id`** → Identificador único. Permite selección directa (`getElementById`) y vínculos internos (`href="#id"`).
    
- **`class`** → Permite agrupar elementos bajo una misma categoría de estilo o comportamiento. Se puede acceder y modificar con `.classList`.
    
- **`slot`** → Atributo usado en **Web Components**. Define una ranura (slot) para insertar contenido dinámico dentro de un componente personalizado.
    
- **`part`** → También usado en Web Components. Permite aplicar estilos desde fuera de un componente a partes internas marcadas con `part="nombre"`.
    

📘 _Nota:_ `slot` y `part` no suelen usarse en proyectos básicos, pero son parte del estándar actual de HTML.

---

### 2️⃣ Atributos de **presentación, estilo y apariencia**

Estos afectan la apariencia visual o estilística del elemento.

- **`title`** → Muestra un tooltip informativo al pasar el puntero.
    
- **`hidden`** → Oculta el elemento completamente del renderizado visual y accesible. Equivale a `display: none`, pero sin usar CSS.
    
- **`style`** → Define estilos **inline** directamente sobre el elemento. Se accede en el DOM mediante la propiedad `.style`.
    
- **`dir`** → Define la dirección del texto (`ltr`, `rtl`, `auto`). Importante para idiomas como árabe o hebreo.
    
- **`lang`** → Especifica el idioma del contenido del elemento, útil para accesibilidad y traducción automática.
    

Ejemplo:

```html
<p lang="es" dir="ltr" title="Texto en español">Hola mundo</p>
```

Estos atributos pueden modificarse con `setAttribute` o directamente con sus propiedades (`element.lang`, `element.hidden`, etc.).

---

### 3️⃣ Atributos de **comportamiento y manejo de eventos**

Estos controlan **cómo se comporta el elemento ante eventos o scripts**.

- **`tabindex`** → Define el orden de tabulación para la navegación con teclado.
    
- **`accesskey`** → Asigna una tecla de acceso directo al elemento.
    
- **`draggable`** → Indica si el elemento se puede arrastrar (`true` o `false`).
    
- **`contenteditable`** → Permite editar el contenido del elemento directamente en el navegador.
    
- **`spellcheck`** → Activa o desactiva el corrector ortográfico del navegador.
    
- **`autocapitalize`** → Controla la capitalización automática del texto en dispositivos móviles.
    
- **`translate`** → Indica si el contenido debe ser traducido automáticamente por el navegador.
    

Ejemplo:

```html
<p contenteditable="true" spellcheck="false" draggable="true">
  Este texto puede editarse, pero no se corrige ortografía.
</p>
```

Desde JavaScript:

```js
const p = document.querySelector("p");
p.setAttribute("contenteditable", "false");
console.log(p.draggable); // true
```

---

### 4️⃣ Atributos de **accesibilidad e interacción**

Estos se usan para mejorar la **accesibilidad (A11Y)** y la interacción con tecnologías asistivas.

- **`aria-*`** → Conjunto de atributos **ARIA (Accessible Rich Internet Applications)**, que describen roles, estados y propiedades de elementos.  
    Ejemplo: `aria-label`, `aria-hidden`, `aria-expanded`, etc.
    
- **`role`** → Define el rol semántico del elemento, como “button”, “navigation”, “dialog”.
    

Ejemplo:

```html
<button role="switch" aria-checked="true">Activado</button>
```

Estos atributos **no cambian el comportamiento visual**, pero son esenciales para lectores de pantalla y navegación por teclado.  
También pueden manipularse desde JavaScript:

```js
const boton = document.querySelector("button");
boton.setAttribute("aria-checked", "false");
```

---

### 5️⃣ Atributos de **datos personalizados**

- **`data-*`** → Permiten agregar información personalizada para scripts.  
    Son interpretados por el DOM como un objeto `dataset`.
    

Ejemplo:

```html
<div data-id="45" data-tipo="usuario"></div>
```

```js
const div = document.querySelector("div");
console.log(div.dataset.tipo); // "usuario"
```

---

## 🧠 Diagrama conceptual: cómo se distribuyen los atributos globales en el DOM

```
[Elemento del DOM]
│
├── Identificación
│   ├─ id
│   ├─ class
│   ├─ slot / part
│
├── Apariencia
│   ├─ style
│   ├─ title
│   ├─ lang / dir / hidden
│
├── Comportamiento
│   ├─ tabindex / accesskey
│   ├─ draggable / contenteditable
│   ├─ spellcheck / translate
│
├── Accesibilidad
│   ├─ role
│   └─ aria-*
│
└── Datos personalizados
    └─ data-*
```

Cada grupo puede manipularse con los **métodos de atributos** (`getAttribute`, `setAttribute`, `removeAttribute`, `hasAttribute`), y sus efectos se reflejan directamente en la **representación del DOM**.

---

## 🧩 Conclusión general

Los atributos globales son un **lenguaje de comunicación entre HTML, CSS, JavaScript y el usuario**.  
Algunos (como `id`, `class` o `data-*`) afectan la forma en que los scripts acceden a los elementos; otros (como `hidden` o `style`) modifican la presentación; y otros (como `aria-*` o `role`) mejoran la accesibilidad.

Saber **cuáles existen y cómo interactúan con el DOM** permite entender la estructura y el comportamiento de cualquier página web a nivel profundo.

---
