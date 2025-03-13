#git #ramas 
## **📌 Introducción a las Ramas en Git**

Las ramas en Git permiten trabajar en diferentes características o correcciones sin afectar el código principal. Son esenciales en cualquier flujo de trabajo colaborativo y en proyectos con múltiples desarrolladores.

## **1️⃣ Conceptos Claves sobre Ramas**

- **Rama (`branch`)**: Una línea de desarrollo separada del código principal.
- **Rama principal (`main` o `master`)**: La rama predeterminada de un repositorio.
- **HEAD**: Referencia actual a la rama activa.
- **Merge**: Proceso de combinar cambios de una rama a otra.
- **Rebase**: Técnica para reestructurar commits sobre una rama base.

## **2️⃣ Flujo Básico de Trabajo con Ramas**

📌 Crear una nueva rama y cambiar a ella:

```sh
git branch feature-nueva
git switch feature-nueva
```

📌 Hacer cambios, agregarlos y confirmarlos:

```sh
git add .
git commit -m "feat: nueva funcionalidad"
```

📌 Volver a la rama principal y fusionar los cambios:

```sh
git switch main
git merge feature-nueva
```

📌 Eliminar una rama después de fusionar:

```sh
git branch -d feature-nueva
```

## **3️⃣ Estrategias de Ramas en Equipos**

🔹 **Feature Branching** (Ramas de Características)

- Se crean ramas para nuevas funcionalidades y se fusionan en `main` después de completarlas.

🔹 **Git Flow**

- Usa ramas `develop`, `feature/*`, `release/*` y `hotfix/*` para controlar el desarrollo.

🔹 **Trunk-Based Development**

- Desarrollo en la rama `main`, usando ramas pequeñas que se fusionan rápidamente.

## **4️⃣ Buenas Prácticas en el Uso de Ramas**

✅ Mantén las ramas pequeñas y enfocadas en una sola tarea. ✅ Usa nombres descriptivos (`fix-bug-login`, `feature-dark-mode`). ✅ Haz `rebase` en lugar de `merge` para evitar commits innecesarios. ✅ Usa `git pull --rebase` para mantener un historial limpio. ✅ Borra ramas después de fusionarlas para evitar desorden.

## **5️⃣ Comandos Avanzados con Ramas**

📌 Ver todas las ramas del repositorio:

```sh
git branch -a
```

📌 Rebasing: Aplicar cambios de una rama sobre otra:

```sh
git switch feature-nueva
git rebase main
```

📌 Fusionar con `squash` para combinar commits:

```sh
git merge --squash feature-nueva
```

📌 Eliminar una rama remota:

```sh
git push origin --delete feature-nueva
```

📌 **Dominar el uso de ramas en Git mejora la organización y eficiencia del equipo. ¡Practica y optimiza tu flujo de trabajo! 🚀**