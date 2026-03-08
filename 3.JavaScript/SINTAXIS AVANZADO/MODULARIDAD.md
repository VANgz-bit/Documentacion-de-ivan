# 📌 Modularidad en JavaScript

## 🔹 Concepto General

La **modularidad** es un principio fundamental en la ingeniería de software que consiste en dividir un programa en **componentes independientes**, llamados _módulos_. Cada módulo concentra una parte específica de la lógica y puede integrarse con otros para construir un sistema más grande.

En el caso de JavaScript, esta capacidad se consolidó a partir de **ES6 (2015)**, gracias a la introducción de las instrucciones **`export`** e **`import`**, que permiten compartir código entre archivos de manera nativa. Antes de este estándar, la modularización dependía de librerías externas como _CommonJS_ (Node.js) o _AMD_.

En términos prácticos, la modularidad favorece la organización, la escalabilidad y la reutilización del código, transformando el desarrollo en un proceso más limpio y sostenible.

---

## 🔹 Justificación de la modularidad

Cuando todo el programa se concentra en un único archivo `.js`, el código tiende a crecer de manera caótica. Esto trae consigo varios problemas:

- **Dificultad de lectura**: localizar un fragmento de código se vuelve lento y confuso.
    
- **Complejidad en el mantenimiento**: corregir errores o agregar nuevas funciones incrementa el riesgo de romper otras partes del sistema.
    
- **Limitada reutilización**: resulta complicado extraer partes de ese archivo para utilizarlas en otros proyectos.
    

La modularidad resuelve estos inconvenientes al **encapsular responsabilidades** en archivos separados. De este modo, cada módulo se ocupa de un aspecto particular (por ejemplo: manejo de usuarios, lógica de productos, funciones de utilidad), y su combinación genera un sistema más estructurado y escalable.

---

## 🔹 Exportación en JavaScript

Un módulo puede **exponer** partes de su código para que otros archivos puedan utilizarlas. Esto se hace mediante la palabra clave **`export`**.

Existen dos modalidades principales:

1. **Exportación nombrada**: se pueden exportar múltiples entidades desde el mismo archivo.
    
2. **Exportación por defecto**: se exporta una única entidad principal.
    

**Ejemplo de exportación nombrada**:

```javascript
// archivo: Material.js
export class Material {
  constructor(titulo, autor) {
    this.titulo = titulo;
    this.autor = autor;
  }

  mostrarInfo() {
    return `${this.titulo} de ${this.autor}`;
  }
}

export const version = "1.0";
```

**Ejemplo de exportación por defecto**:

```javascript
// archivo: Utilidades.js
export default function saludar(nombre) {
  console.log(`Hola, ${nombre}`);
}
```

---

## 🔹 Importación en JavaScript

La **importación** permite traer al archivo local aquellas entidades que fueron exportadas en otros módulos. Esto se realiza con la palabra clave **`import`**.

**Ejemplo de importación nombrada**:

```javascript
import { Material, version } from "./Material.js";

const libro = new Material("El Principito", "Saint-Exupéry");
console.log(libro.mostrarInfo());
console.log(version);
```

**Ejemplo de importación por defecto**:

```javascript
import saludar from "./Utilidades.js";

saludar("Iván");
```

En este último caso no se utilizan llaves `{}`, ya que se trata de la exportación principal.

---

## 🔹 El rol de `type="module"`

El navegador no interpreta automáticamente el sistema de módulos de ES6. Es necesario declarar explícitamente que un archivo debe tratarse como módulo mediante el atributo **`type="module"`** en la etiqueta `<script>` de un documento HTML:

```html
<script type="module" src="main.js"></script>
```

Gracias a esto, el navegador reconoce las instrucciones `import` y `export`, estableciendo la modularidad de manera nativa.

---

## 🔹 Ejemplo integrado

Imaginemos un sistema simple para organizar una biblioteca.

**Archivo `Material.js`:**

```javascript
export class Material {
  constructor(titulo, autor) {
    this.titulo = titulo;
    this.autor = autor;
  }

  mostrarInfo() {
    return `${this.titulo} de ${this.autor}`;
  }
}
```

**Archivo `Libro.js`:**

```javascript
import { Material } from "./Material.js";

export class Libro extends Material {
  constructor(titulo, autor, paginas) {
    super(titulo, autor);
    this.paginas = paginas;
  }

  mostrarInfo() {
    return `📖 ${this.titulo} (${this.paginas} páginas) - ${this.autor}`;
  }
}
```

**Archivo `main.js`:**

```javascript
import { Libro } from "./Libro.js";

const libro1 = new Libro("El Principito", "Saint-Exupéry", 96);
console.log(libro1.mostrarInfo());
```

**Archivo `index.html`:**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo Modularidad</title>
</head>
<body>
  <h1>Ejemplo de módulos en JavaScript</h1>
  <script type="module" src="main.js"></script>
</body>
</html>
```

Resultado en la consola:

```
📖 El Principito (96 páginas) - Saint-Exupéry
```

---

## 🔹 Conclusión

La modularidad en JavaScript no es solo una herramienta técnica, sino un principio de diseño que transforma la manera en que se construyen las aplicaciones. Su adopción permite **organizar el código en partes reutilizables y mantenibles**, reducir la complejidad y preparar los proyectos para crecer de manera controlada.

Hoy constituye un estándar en el desarrollo web profesional y es la base para arquitecturas más complejas como los **frameworks modernos** (React, Angular, Vue), que dependen en gran medida de esta estructura modular.

---
