
###  1. **Comandos de consola / terminal / línea de comandos**

Ese es el nombre general. Se refieren a **instrucciones que ejecutás desde una terminal** para interactuar con el sistema operativo sin usar la interfaz gráfica (sin hacer clics, solo con texto).

---

##  Clasificación por tipo de acción

Dentro de los **comandos de terminal**, se pueden clasificar en distintas **categorías** o **tipos funcionales**:

|Categoría|Qué hace|Ejemplos|
|---|---|---|
|🗃 **Gestión de archivos y carpetas**|Crear, borrar, copiar, mover, listar|`cd`, `ls`, `mkdir`, `rm`, `mv`, `cp`|
|📍 **Navegación**|Moverse entre carpetas o ver ubicación actual|`cd`, `pwd`|
|📄 **Manipulación de contenido**|Ver o buscar dentro de archivos|`cat`, `head`, `tail`, `grep`, `less`, `nano`|
|🔐 **Permisos y propietarios**|Cambiar quién puede acceder o modificar archivos|`chmod`, `chown`, `chgrp`|
|🛠 **Gestión del sistema**|Monitorear o controlar procesos|`top`, `ps`, `kill`, `df`, `free`|
|📦 **Compresión y archivos**|Comprimir o descomprimir archivos|`zip`, `unzip`, `tar`, `gzip`|
|🧹 **Utilitarios**|Limpieza o información útil|`clear`, `history`, `date`, `whoami`|
|🧪 **Comandos administrativos (requieren permisos)**|Control del sistema a nivel de administrador|`sudo`, `reboot`, `shutdown`, `apt` (en Linux)|

---

## ¿Qué nombre técnico tienen?

Según el sistema operativo, estos comandos se conocen como:

|Sistema|Nombre técnico|
|---|---|
|🐧 Linux / macOS|**Unix shell commands** o **comandos de Bash**|
|🪟 Windows|**Comandos CMD** o **PowerShell commands**|

**📂 GUÍA COMPLETA DE COMANDOS DE TERMINAL - CLASIFICADOS Y DESARROLLADOS**

---

# 📃 1. GESTIÓN DE ARCHIVOS Y CARPETAS

**Comandos para crear, borrar, mover, renombrar y copiar archivos o carpetas.**

### ✅ Crear archivos o carpetas

- `mkdir nombre_carpeta`: crea una carpeta.
    
- `touch archivo.txt`: crea un archivo vacío.
    

### ❌ Eliminar archivos o carpetas

- `rm archivo.txt`: elimina un archivo.
    
- `rm -r carpeta/`: elimina una carpeta y su contenido.
    
- `rm -rf carpeta/`: elimina sin pedir confirmación (peligroso).
    
- `rm -i archivo.txt`: elimina con confirmación.
    

### 📁 Mover o renombrar archivos o carpetas

- `mv archivo.txt carpeta/`: mueve un archivo a una carpeta.
    
- `mv viejo.txt nuevo.txt`: renombra el archivo.
    
- `mv archivo.txt nueva_carpeta/nuevo_nombre.txt`: mueve y renombra.
    

### 📄 Copiar archivos o carpetas

- `cp archivo.txt copia.txt`: copia archivo.
    
- `cp archivo.txt carpeta/`: copia archivo a otra carpeta.
    
- `cp -r carpeta1 carpeta2`: copia una carpeta completa.
    

---

# 📍 2. NAVEGACIÓN ENTRE CARPETAS

**Comandos para moverse por el sistema de archivos.**

### 📂 Entrar en carpetas

- `cd carpeta`: entra a la carpeta.
    
- `cd ~/Documentos`: entra a Documentos desde cualquier parte.
    

### ⬆️ Salir o retroceder

- `cd ..`: sube un nivel.
    
- `cd ../..`: sube dos niveles.
    
- `cd -`: vuelve a la carpeta anterior exacta.
    

### 🌐 Otras ubicaciones comunes

- `cd ~`: va al directorio personal del usuario.
    
- `cd /`: va a la raíz del sistema.
    

### 📅 Ver contenido de una carpeta

- `ls`: lista archivos y carpetas.
    
- `ls -l`: lista con detalles.
    
- `ls -a`: incluye archivos ocultos.
    
- `ls -la`: todo junto.
    
- `ls carpeta`: muestra contenido sin entrar.
    

### 📍 Ver ubicación actual

- `pwd`: muestra la ruta absoluta de la carpeta actual.
    

---

# 📄 3. CONTENIDO DE ARCHIVOS

**Ver, buscar y editar archivos desde la terminal.**

### 📃 Ver contenido

- `cat archivo.txt`: muestra el archivo completo.
    
- `head archivo.txt`: muestra las primeras 10 líneas.
    
- `tail archivo.txt`: muestra las últimas 10 líneas.
    
- `tail -f archivo.log`: muestra en tiempo real lo que se agrega.
    

### 🔍 Buscar dentro de archivos

- `grep "texto" archivo.txt`: busca líneas que contengan esa palabra.
    

### 🖊️ Editar archivos (modo texto)

- `nano archivo.txt`: editor simple.
    
- `vim archivo.txt`: editor avanzado.
    
- `code .`: abre Visual Studio Code (si está instalado).
    

---

# 🔐 4. PERMISOS Y PROPIETARIOS

**Modificar accesos a archivos y cambiar dueños.**

### ⛨️ Cambiar permisos

- `chmod 755 archivo`: permisos completos al usuario, lectura/ejecución al resto.
    

|Dígito|Permisos|Significado|
|---|---|---|
|7|rwx|leer, escribir, ejecutar|
|6|rw-|leer, escribir|
|5|r-x|leer, ejecutar|
|4|r--|solo lectura|
|0|---|sin permisos|

### 🧑‍💼 Cambiar propietario

- `sudo chown ivan archivo.txt`: asigna nuevo dueño.
    

### 🔒 Proteger archivos

- `chattr +i archivo.txt`: impide borrar o editar (Linux).
    

---

# 🚼 5. UTILITARIOS DE LA TERMINAL

**Comandos para limpieza, información y ayuda.**

- `clear`: limpia la pantalla.
    
- `date`: muestra fecha y hora.
    
- `whoami`: muestra el nombre del usuario.
    
- `history`: historial de comandos.
    
- `TAB`: autocompleta nombres.
    
- ↑ / ↓: navega por comandos anteriores.
    

---

# 📊 6. ADMINISTRACIÓN DEL SISTEMA

**Supervisión de recursos y control de procesos.**

- `top`: monitor en tiempo real de procesos.
    
- `kill 1234`: termina el proceso con ID 1234.
    
- `df -h`: espacio en disco.
    
- `free -h`: uso de memoria RAM.
    

---

# 📆 7. COMPRESIÓN Y ARCHIVOS ZIP

**Empaquetar o extraer archivos comprimidos.**

- `zip archivo.zip archivo.txt`: comprimir archivo.
    
- `unzip archivo.zip`: descomprimir archivo.
    
- `tar -czvf archivo.tar.gz carpeta/`: comprimir carpeta.
    
- `tar -xzvf archivo.tar.gz`: descomprimir.
    
- `tar -tzf archivo.tar.gz`: ver contenido sin descomprimir.
    

---

# ⚡ 8. COMANDOS ADMINISTRATIVOS (CON SUDO)

**Requieren permisos de superusuario (administrador).**

- `sudo`: ejecutar comando como admin.
    
- `sudo reboot`: reiniciar el sistema.
    
- `sudo shutdown now`: apagar ahora.
    
- `sudo shutdown -h +10`: apagar en 10 minutos.
    
- `sudo apt update`: actualizar paquetes (Linux Debian/Ubuntu).
    

---