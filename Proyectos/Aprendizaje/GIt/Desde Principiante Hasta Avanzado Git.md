## Introduccion #git 

Git es un sistema de control de versiones que permite gestionar el historial de cambios en pyotectos de software.

---

## **Capítulo 1: Conceptos Básicos de Git** 

### **1.1 Instalación y Configuración Inicial**

Para comenzar con Git, primero debemos instalarlo:

- **Windows:** Descargar desde [git-scm.com](https://git-scm.com/)
- **Linux:**
    
    ```sh
    sudo apt install git # Debian/Ubuntu
    sudo dnf install git # Fedora
    sudo pacman -S git   # Arch Linux
    ```
    
- **macOS:**
    
    ```sh
    brew install git
    ```
    

Después de instalar Git, configúralo con:

```sh
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
```

### **1.2 Iniciando un Repositorio**

```sh
git init
```

Esto crea un repositorio vacío en la carpeta actual.

### **1.3 Estados de Git**

- **Untracked:** Archivo nuevo sin seguimiento.
- **Staged:** Archivo agregado para commit.
- **Committed:** Archivo guardado en el historial.

Para ver el estado:

```sh
git status
```

### **1.4 Ciclo de Trabajo en Git**

1. Modificas archivos.
2. Los agregas al área de preparación (`git add`).
3. Los confirmas con un commit (`git commit`).
4. Los envías al repositorio remoto (`git push`).

Ejemplo:

```sh
git add .
git commit -m "feat: agregar funcionalidad X"
git push origin main
```

---

## **Capítulo 2: Trabajo con Ramas**

### **2.1 Creación y Cambio de Ramas**

```sh
git branch nueva-rama
git checkout nueva-rama
# o
git switch nueva-rama
```

### **2.2 Fusionar Ramas (Merge)**

```sh
git checkout main
git merge nueva-rama
```

### **2.3 Rebasing**

```sh
git rebase main
```

---

## **Capítulo 3: Git Avanzado**

### **3.1 Revertir Cambios**

```sh
git revert HEAD # Revierte el último commit
```

### **3.2 Stashing (Guardar Temporalmente Cambios)**

```sh
git stash
```

### **3.3 Cherry-picking (Seleccionar Commits Específicos)**

```sh
git cherry-pick <commit-id>
```

### **3.4 Tags (Versiones en Git)**

```sh
git tag -a v1.0 -m "Versión 1.0"
git push origin v1.0
```

---

## **Capítulo 4: Mejores Prácticas** 

- Hacer commits pequeños y con mensajes claros.
- Usar ramas para nuevas funcionalidades (`feature/nombre`).
- Evitar `git push --force` en ramas compartidas.
- Hacer `pull` antes de `push` para evitar conflictos.
- Revisar cambios antes de confirmarlos con `git diff`.

---

Este libro es una referencia completa para que puedas dominar Git. 📚