## 📘 Introducción a la Navegación de Nodos en el DOM

### 🔹 Qué significa “navegar el DOM”

El **Document Object Model (DOM)** se estructura como un **árbol jerárquico**, donde cada elemento, texto o comentario del documento HTML corresponde a un **nodo**.  
“Navegar el DOM” significa **movernos entre esos nodos** para acceder a ellos, leer su información o modificarlos según su relación dentro de la jerarquía.

Podemos desplazarnos **hacia abajo** (accediendo a hijos), **hacia arriba** (accediendo al padre), o **horizontalmente** (accediendo a hermanos).  
Estas tres direcciones conforman la base de la _navegación del árbol DOM_.

---

### 🔹 Relaciones jerárquicas entre nodos

Cada nodo en el DOM tiene una posición y relaciones definidas con otros nodos:

```
document
 └── html
      ├── head
      │    └── title
      └── body
           ├── header
           ├── main
           │    ├── section
           │    └── article
           └── footer
```

En este ejemplo:

- `html` es el **nodo raíz**.
    
- `head` y `body` son **hijos** de `html`.
    
- `main` es **padre** de `section` y `article`.
    
- `section` y `article` son **hermanos** entre sí.
    

---

### 🔹 Tipos de relaciones principales

1. **Relación padre-hijo:**  
    Un nodo puede contener uno o varios hijos.  
    Ejemplo: `<ul>` es padre de sus `<li>`.
    
2. **Relación hijo-padre:**  
    Cada nodo, excepto el raíz (`document`), tiene un padre que lo contiene.
    
3. **Relación entre hermanos:**  
    Son nodos que comparten el mismo padre.  
    Ejemplo: dos `<li>` dentro del mismo `<ul>`.
    

---

### 🔹 Importancia de la navegación en el DOM

Comprender y manipular estas relaciones permite:

- Acceder directamente a nodos sin buscarlos por selectores.
    
- Crear, mover o eliminar elementos con precisión estructural.
    
- Optimizar operaciones dinámicas (como recorrer listas o secciones).
    
- Realizar verificaciones de jerarquía (por ejemplo, comprobar si un nodo pertenece a otro).
    

A diferencia de los **métodos de selección** (`getElementById()`, `querySelector()`), que buscan elementos por su nombre o atributos, **las propiedades de navegación** parten de un nodo ya obtenido y permiten moverse **a través del árbol**, explorando sus conexiones naturales.

---

### 🔹 En qué consiste este bloque

A partir de esta introducción, se profundizará en tres secciones consecutivas:

1. **Obtención y modificación de hijos (childs)**  
    → Cómo acceder, recorrer y manipular los nodos descendientes de un elemento.
    
2. **Propiedades de padres (parents)**  
    → Cómo subir en la jerarquía desde un nodo hijo hasta su contenedor inmediato.
    
3. **Propiedades de hermanos (siblings)**  
    → Cómo desplazarse lateralmente entre nodos que comparten el mismo nivel jerárquico.
    

Estas tres relaciones forman el núcleo de la navegación dentro del DOM y permiten comprender cómo se organiza y se interconecta la estructura de un documento web.

---
