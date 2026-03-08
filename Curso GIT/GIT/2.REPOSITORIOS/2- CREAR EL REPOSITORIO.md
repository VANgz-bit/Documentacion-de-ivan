
## **Cómo crear una carpeta como repositorio en Git**

Para iniciar el control de versiones en un proyecto local con Git, es necesario convertir una carpeta común en un **repositorio Git**. Esto se hace siguiendo una serie de pasos claros y utilizando comandos específicos desde la terminal o consola.

---

### **1. Crear una carpeta para el proyecto**

Primero, se necesita tener una carpeta donde se almacenarán los archivos del proyecto. Puede ser una carpeta nueva o una ya existente.

**Comando:**

```bash
mkdir nombre-de-la-carpeta
```

Este comando crea una nueva carpeta con el nombre especificado.

---

### **2. Entrar en la carpeta**

Una vez creada (o localizada) la carpeta, se debe acceder a ella con el siguiente comando:

**Comando:**

```bash
cd nombre-de-la-carpeta
```

Esto posiciona la terminal dentro de esa carpeta.

---

### **3. Inicializar el repositorio**

Dentro de la carpeta, se inicializa el repositorio de Git con:

**Comando:**

```bash
git init
```

**¿Qué hace este comando?**

- Crea una subcarpeta oculta llamada `.git`.
    
- Esta carpeta contiene toda la información interna que Git necesita para realizar el seguimiento del proyecto: historial de cambios, configuración, objetos, referencias, etc.
    
- A partir de este punto, Git puede empezar a registrar cambios dentro de esta carpeta.
    

---

### **4. Verificar que el repositorio fue creado correctamente**

Se puede comprobar que Git fue inicializado con éxito utilizando:

**Comando:**

```bash
ls -a
```

Este comando muestra los archivos ocultos. Si `.git` aparece en la lista, el repositorio está correctamente inicializado.

---

### **5. Estado inicial del repositorio**

Para conocer el estado del repositorio y ver qué archivos hay listos o no para ser gestionados por Git, se usa:

**Comando:**

```bash
git status
```

Este comando indica:

- Si hay archivos sin seguimiento (untracked),
    
- Si hay archivos preparados para confirmar (staged),
    
- Si no hay cambios registrados aún.
    

---

### **Resumen de comandos utilizados**

|Acción|Comando|
|---|---|
|Crear carpeta|`mkdir nombre-de-la-carpeta`|
|Entrar a la carpeta|`cd nombre-de-la-carpeta`|
|Inicializar repositorio Git|`git init`|
|Ver archivos ocultos|`ls -a`|
|Ver estado del repositorio|`git status`|

---

### **Notas adicionales**

- Inicializar un repositorio no sube los archivos a ningún servidor remoto como GitHub; simplemente se habilita el control de versiones local.
    
- Es posible continuar agregando archivos, hacer commits y luego conectar este repositorio a un remoto si se desea.
