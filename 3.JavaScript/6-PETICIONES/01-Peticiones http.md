## ¿Qué son las **Peticiones HTTP**?

Las **peticiones HTTP** son mensajes que se envían a través del protocolo **HTTP (HyperText Transfer Protocol)** para **solicitar o enviar información** entre dos partes:

- **Cliente**
    
- **Servidor**
    

Este intercambio es la base de **cómo funciona la web**.

> Cada vez que se carga una página, se envía un formulario o se obtienen datos desde una API, ocurre una petición HTTP.

---

## ¿Quién es el **cliente**?

### Definición

El **cliente** es la aplicación que **inicia la comunicación** y **realiza la petición**.

En desarrollo web, el cliente suele ser:

- El **navegador web** (Chrome, Firefox, Edge)
    
- Una aplicación frontend (hecha con HTML, CSS y JavaScript)
    
- Una app móvil o de escritorio
    

### ¿Qué hace el cliente?

El cliente:

- Solicita recursos (HTML, CSS, JS, imágenes, datos, etc.)
    
- Envía información al servidor (formularios, credenciales, datos JSON)
    
- Interpreta y muestra la respuesta del servidor
    

### Ejemplo conceptual

Cuando se escribe una URL en el navegador:

```text
https://api.ejemplo.com/usuarios
```

El navegador (cliente) está diciendo:

> “Servidor, dame la información de los usuarios”.

---

## ¿Quién es el **servidor**?

### Definición

El **servidor** es el sistema que:

- **Recibe** las peticiones del cliente
    
- **Procesa** la solicitud
    
- **Devuelve** una respuesta
    

El servidor puede ser:

- Un servidor web (Apache, Nginx)
    
- Una aplicación backend (Node.js, Java, Python, PHP)
    
- Un servicio externo (APIs públicas)
    

### ¿Qué hace el servidor?

El servidor:

- Decide si la petición es válida
    
- Accede a bases de datos
    
- Aplica lógica de negocio
    
- Envía una respuesta adecuada
    

---

## Relación Cliente – Servidor (bien gramatizada)

Podemos expresarlo correctamente así:

> El **cliente** envía una **petición HTTP** al **servidor**, y el **servidor** responde con un **mensaje HTTP** que contiene la información solicitada o el resultado de la operación.

Este intercambio se llama **modelo cliente-servidor**.

---

## ¿Guardan información el cliente y el servidor?

Esta es una **pregunta muy importante**.

### 1. ¿El cliente guarda información?

**Sí, pero de forma limitada.**

El cliente puede guardar información como:

- Cookies
    
- LocalStorage
    
- SessionStorage
    
- Cache del navegador
    

Ejemplos:

- Mantener una sesión iniciada
    
- Guardar preferencias del usuario
    
- Almacenar datos temporales
    

⚠️ El cliente **no es seguro** para datos sensibles.

---

### 2. ¿El servidor guarda información?

**Sí, y es el lugar principal donde se guarda la información importante.**

El servidor puede almacenar:

- Usuarios
    
- Contraseñas (encriptadas)
    
- Publicaciones
    
- Productos
    
- Historiales
    
- Configuraciones
    

Esto se hace generalmente en:

- Bases de datos (MySQL, PostgreSQL, MongoDB)
    
- Sistemas de archivos
    
- Servicios externos
    

---

## Punto clave: HTTP es **sin estado** (stateless)

Por defecto:

> **HTTP no recuerda peticiones anteriores.**

Cada petición es independiente.

Entonces:

- El servidor **no recuerda automáticamente** al cliente
    
- Para “recordar” algo se usan mecanismos como:
    
    - Cookies
        
    - Tokens
        
    - Sesiones
        

Esto conecta directamente con lo que más adelante vas a ver en **auth**, **APIs** y **fetch**.

---

## Ejemplo simple del flujo completo

1. El cliente hace una petición HTTP
    
2. El servidor la recibe
    
3. El servidor consulta datos (si hace falta)
    
4. El servidor responde
    
5. El cliente usa la respuesta (mostrar datos, actualizar la UI)
    

---

## Resumen conceptual

- **Peticiones HTTP**: mensajes para intercambiar información en la web.
    
- **Cliente**: inicia la comunicación.
    
- **Servidor**: responde y maneja los datos.
    
- **Cliente guarda info**: sí, pero limitada y no segura.
    
- **Servidor guarda info**: sí, es el lugar principal.
    
- **HTTP es stateless**: no guarda estado por sí solo.
    

---
