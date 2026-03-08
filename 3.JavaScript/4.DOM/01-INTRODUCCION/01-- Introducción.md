# 📄 `que-es-el-dom.md`

## 🧩 ¿Qué es el DOM?

El **DOM** (Document Object Model) o **Modelo de Objetos del Documento** es una **representación estructurada en forma de árbol** que el navegador crea a partir del **código HTML (o XML)** de una página web.

Cuando un navegador carga una página, **interpreta el HTML** y **genera una estructura de objetos en memoria**, donde **cada etiqueta, texto o comentario** se convierte en un **nodo** dentro de ese árbol.  
De esta manera, el DOM **traduce el documento estático en una representación viva**, con la cual **JavaScript** puede **interactuar, leer o modificar**.

Podemos imaginar el DOM como una **versión programable del documento HTML**, en la que cada elemento puede ser accedido y manipulado mediante código.

---

## ⚙️ ¿Cómo se genera el DOM?

1. El navegador **descarga el archivo HTML**.
    
2. El **motor de renderizado** del navegador (por ejemplo, Blink en Chrome o Gecko en Firefox) **analiza el documento línea por línea**.
    
3. A medida que lee las etiquetas, **crea objetos en memoria** que representan cada elemento y su relación con otros.
    
4. Estos objetos se **organizan jerárquicamente** formando un **árbol de nodos**, donde el nodo raíz es siempre `document`.
    
5. Este árbol queda disponible a través del **objeto global `document`** en JavaScript.
    

El proceso completo puede representarse así:

---

### 📊 Diagrama del proceso de creación del DOM

```
HTML Original (archivo .html)
         ↓
   [ Parser HTML del navegador ]
         ↓
  Estructura de objetos (DOM Tree)
         ↓
  Interfaz accesible vía JavaScript
```

O visualmente:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Mi página</title>
  </head>
  <body>
    <h1>Hola Mundo</h1>
    <p>Bienvenido al DOM</p>
  </body>
</html>
```

⬇️ se transforma en ⬇️

```
Document
│
├── html
│   ├── head
│   │   └── title
│   │        └── "Mi página"
│   │
│   └── body
│        ├── h1
│        │    └── "Hola Mundo"
│        │
│        └── p
│             └── "Bienvenido al DOM"
```

Este **árbol DOM** es lo que el navegador mantiene en memoria.  
Cada etiqueta HTML se convierte en un **nodo de tipo elemento**, y los textos dentro de ellas se convierten en **nodos de tipo texto**.

---

## 🔄 Relación entre HTML, DOM y Renderizado

Es fundamental entender que el **DOM no es el HTML**, sino una **representación viva** de él.

- El **HTML** es el archivo fuente (texto plano).
    
- El **DOM** es la estructura que el navegador construye a partir de ese HTML.
    
- Y el **Render Tree** es la estructura visual usada por el navegador para dibujar los elementos en pantalla (interviene el CSS y el layout).
    

Esto implica que si **modificamos el DOM con JavaScript**, **el HTML original no cambia**, pero **la página visible sí**, porque el navegador vuelve a renderizar el área afectada.

---

## 🧠 Ejemplo comparativo

HTML original:

```html
<p id="texto">Hola Mundo</p>
```

DOM en memoria (representación conceptual):

```
Document
└── html
     └── body
          └── p (id="texto")
               └── "Hola Mundo"
```

Si desde JavaScript ejecutamos:

```js
document.getElementById("texto").textContent = "DOM Modificado";
```

El árbol DOM cambia, y el navegador actualiza la vista:

```
<p id="texto">DOM Modificado</p>
```

> 🔎 El archivo HTML en el servidor sigue igual, pero el DOM en memoria fue modificado dinámicamente.

---

## 💬 Importancia del DOM

El DOM es la **puerta de entrada de JavaScript al documento web**.  
A través de él podemos:

- Acceder, crear o eliminar elementos del documento.
    
- Cambiar atributos, clases o estilos.
    
- Escuchar y responder a eventos (clicks, teclas, scroll, etc.).
    
- Controlar o animar partes del contenido sin recargar la página.
    

En otras palabras, el DOM convierte un documento estático en una **experiencia interactiva y dinámica**.

---

## 🧭 Resumen gráfico conceptual

```
[ HTML ]
   ↓ (Interpretado por el navegador)
[ DOM ]
   ↓ (Manipulado por JavaScript)
[ Página interactiva ]
```

---
