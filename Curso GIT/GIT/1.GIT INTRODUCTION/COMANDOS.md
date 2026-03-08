
##  COMANDOS FUNDAMENTALES 

- `git init`: Inicializa un repositorio.
    
- `git status`: Muestra el estado de los archivos.
    
- `git add`: Prepara archivos para el commit.
    
- `git commit`: Registra los cambios en el historial.
    
- `git restore`: Deshace cambios en archivos o staging.
    
- `git reset`: Quita del staging, mueve el HEAD o revierte commits.
    
- `git checkout`: Cambia ramas o recupera archivos (reemplazado en parte por `switch` y `restore`).
    
- `git mv`: Renombra archivos.
    
- `git rm`: Elimina archivos del repositorio y del sistema de archivos.
    

---

##  RAMAS Y VERSIONADO

- `git branch`: Crea, lista o borra ramas.
    
- `git switch`: Cambia entre ramas (reemplaza parte de `checkout`).
    
- `git merge`: Une cambios de una rama a otra.
    
- `git rebase`: Reescribe la historia de commits (más avanzado que merge).
    
- `git tag`: Crea etiquetas para marcar versiones específicas (como versiones de producción).
    

---

##  TRABAJO CON REMOTOS (GitHub, GitLab, etc.)

- `git remote`: Administra conexiones con repositorios remotos.
    
- `git clone`: Crea una copia local de un repositorio remoto.
    
- `git fetch`: Trae commits nuevos del remoto sin aplicar cambios.
    
- `git pull`: Trae y **fusiona** cambios del remoto.
    
- `git push`: Envía commits locales al servidor remoto.
    

---

##  EXPLORACIÓN Y COMPARACIÓN

- `git log`: Muestra el historial de commits.
    
- `git diff`: Muestra las diferencias entre versiones de archivos.
    
- `git show`: Muestra detalles de un commit específico.
    
- `git blame`: Muestra qué línea fue modificada por qué commit/aut@r.
    

---

##  HERRAMIENTAS AVANZADAS

- `git stash`: Guarda temporalmente cambios no confirmados para limpiar el área de trabajo.
    
- `git cherry-pick`: Copia un commit específico de otra rama y lo aplica en la actual.
    
- `git revert`: Crea un nuevo commit que deshace los cambios de uno anterior (sin eliminar historial).
    
- `git bisect`: Ayuda a encontrar el commit exacto donde se introdujo un error (debug).
    
- `git reflog`: Muestra todos los movimientos recientes del HEAD (útil para recuperar commits perdidos).
    

---

##  CONFIGURACIÓN Y UTILIDADES

- `git config`: Administra la configuración global o local del repositorio.
    
- `git init`: Crea un nuevo repositorio vacío.
    
- `.gitignore`: Archivo especial para excluir archivos de Git.
    
- `.gitattributes`: Define cómo manejar archivos en términos de texto, binarios, saltos de línea, etc.
    

---

##  Resumen

- **Comandos esenciales (básicos):** `add`, `commit`, `status`, `restore`, `reset`, `checkout`, `mv`.
    
- **Comandos de flujo de trabajo en ramas:** `branch`, `merge`, `switch`, `rebase`.
    
- **Comandos de colaboración:** `clone`, `pull`, `push`, `remote`, `fetch`.
    
- **Comandos de análisis y control:** `log`, `diff`, `stash`, `revert`, `reflog`.
