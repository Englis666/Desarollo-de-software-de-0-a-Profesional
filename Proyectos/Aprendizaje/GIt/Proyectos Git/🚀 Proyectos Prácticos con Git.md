
## **1️⃣ Repositorio Personal de Notas** #git #proyectosPracticosGit
📌 **Objetivo:** Usar Git para gestionar notas y documentos en Markdown.

🔹 **Pasos:**

1. Crear un directorio `notas/` y inicializar un repositorio Git.
2. Agregar y versionar archivos `.md`.
3. Configurar `.gitignore` para excluir archivos temporales.
4. Sincronizar con un repositorio remoto en GitHub o GitLab.

🔗 **Comandos clave:**

```sh
git init
git add .
git commit -m "feat: primera versión de mis notas"
git remote add origin <url-repo>
git push -u origin main
```

---

## **2️⃣ Portafolio con GitHub Pages**

📌 **Objetivo:** Crear y desplegar un portafolio con GitHub Pages.

🔹 **Pasos:**

1. Crear un repositorio en GitHub con el nombre `mi-portafolio`.
2. Subir archivos HTML/CSS/JS.
3. Activar GitHub Pages en la configuración del repositorio.
4. Realizar cambios y actualizaciones con Git.

🔗 **Comandos clave:**

```sh
git add .
git commit -m "feat: actualización del portafolio"
git push origin main
```

📌 **Resultado:** Accede a tu portafolio en `https://tuusuario.github.io/mi-portafolio`.

---

## **3️⃣ Simulación de Trabajo en Equipo**

📌 **Objetivo:** Practicar la colaboración en un repositorio compartido.

🔹 **Pasos:**

1. Crear una rama para desarrollar una nueva funcionalidad.
2. Hacer commits con cambios.
3. Enviar la rama al repositorio remoto y hacer un Pull Request.
4. Revisar y fusionar la rama en `main`.

🔗 **Comandos clave:**

```sh
git branch feature-nueva
git switch feature-nueva
git add .
git commit -m "feat: nueva funcionalidad"
git push origin feature-nueva
```

---

## **4️⃣ Automatización con Git Hooks**

📌 **Objetivo:** Mejorar el flujo de trabajo con scripts automatizados en Git.

🔹 **Ejemplo:** Crear un hook `pre-commit` para evitar `console.log` en código JavaScript.

```sh
#!/bin/sh
if git diff --cached | grep 'console.log'; then
    echo "❌ ¡No uses console.log en commits!"
    exit 1
fi
```

🔹 **Pasos:**

1. Guardar el script en `.git/hooks/pre-commit` y darle permisos de ejecución.
2. Hacer un commit y verificar que el hook se ejecuta automáticamente.

---

📌 **Estos proyectos te ayudarán a aplicar Git en el mundo real. ¡Manos a la obra! 🚀**