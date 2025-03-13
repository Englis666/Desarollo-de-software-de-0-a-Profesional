
## **1️⃣ Configuración Inicial** #gitSnippets #git

📌 Configurar usuario globalmente:

```sh
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
git config --global core.editor "vim"
```

📌 Ver configuración:

```sh
git config --list
```

---

## **2️⃣ Flujo de Trabajo Básico**

📌 Inicializar un repositorio y hacer el primer commit:

```sh
git init
git add .
git commit -m "feat: primera versión del proyecto"
```

📌 Subir cambios a un repositorio remoto:

```sh
git remote add origin <url-repo>
git push -u origin main
```

---

## **3️⃣ Trabajo con Ramas**

📌 Crear y cambiar de rama:

```sh
git branch nueva-rama
git switch nueva-rama
```

📌 Fusionar ramas:

```sh
git switch main
git merge nueva-rama
```

📌 Eliminar una rama:

```sh
git branch -d nueva-rama
```

---

## **4️⃣ Revisión de Historial**

📌 Ver historial de commits:

```sh
git log --oneline --graph --decorate
```

📌 Ver diferencias entre commits:

```sh
git diff HEAD~1
```

📌 Ver quién modificó una línea específica:

```sh
git blame archivo.txt
```

---

## **5️⃣ Deshacer Cambios**

📌 Resetear archivo antes de hacer commit:

```sh
git restore archivo.txt
```

📌 Deshacer último commit (manteniendo cambios en el directorio de trabajo):

```sh
git reset --soft HEAD~1
```

📌 Deshacer último commit y cambios:

```sh
git reset --hard HEAD~1
```

---

## **6️⃣ Stash: Guardar Cambios Temporalmente**

📌 Guardar cambios sin hacer commit:

```sh
git stash
```

📌 Recuperar cambios guardados:

```sh
git stash pop
```

---

## **7️⃣ Cherry-Picking y Alias Útiles**

📌 Aplicar un commit específico a otra rama:

```sh
git cherry-pick <commit-hash>
```

📌 Crear alias para comandos frecuentes:

```sh
git config --global alias.st "status -s"
git config --global alias.ci "commit -m"
```

📌 Usar alias:

```sh
git st  # Equivalente a 'git status -s'
git ci "fix: corregido bug en login"  # Equivalente a 'git commit -m'
```

---

📌 **Estos snippets mejorarán tu productividad con Git. ¡A probarlos! 🚀**