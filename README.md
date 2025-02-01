# 🚀 Buenas Prácticas en Git

Este **README** constituye una guía de buenas prácticas para desarrollar proyectos en equipo utilizando **Git**.

---

## 🌱 Estructura de Ramas
Todo proyecto de desarrollo de software debe tener como mínimo **4 ramas principales**:
---

![image](https://github.com/user-attachments/assets/7ac7942d-4fda-4fd5-bceb-1b0fed8aaa55)

---
### 🔹 `main` / `master`
📌 **Producción** | 🚀 **Versión estable**
- Es la rama más delicada porque impacta directamente al cliente.
- Solo recibe cambios cuando se libera una nueva versión estable.

### 🔹 `release`
🛠 **Preparación de versión** | 🔍 **Pruebas previas**
- Se crea a partir de `develop` cuando se prepara una nueva versión para producción.
- Permite realizar pruebas y corregir errores antes del lanzamiento.
- Una vez aprobada, se fusiona en `main` y `develop`.

### 🔹 `develop`
🧪 **Desarrollo principal** | ⚡ **Integración de cambios**
- Se fusionan las funcionalidades (`feature/*`) una vez completadas.
- Es una versión intermedia e inestable.
- No se despliega en producción directamente.

### 🔹 `feature/*`
✨ **Nuevas funcionalidades** | 🔄 **Trabajo en equipo**
- Son ramas individuales para cada tarea o mejora.
- Una vez terminadas, se fusionan en `develop`.

---

## ⚠️ Reglas Clave
🚨 **Antes de hacer `push` (subir cambios), haz `pull` (descargar cambios) y resuelve conflictos.**






---

## 🔄 Flujo de Trabajo comienza en la rama feature

1️⃣ **Crear una rama `feature/*` desde `develop`**
```sh
git checkout develop #ubicarse en la rama develop
git pull origin develop #descargar los cambios remotos
git checkout -b feature/nueva-funcionalidad # añadir una nueva rama y moverte hacía ella
```

2️⃣ **Trabajar en la funcionalidad y hacer commits**
```sh
git add .
git commit -m "Implementación de nueva funcionalidad"
```

3️⃣ **Fusionar `feature/*` en `develop` cuando esté lista**
```sh
git checkout develop
git pull origin develop
git merge feature/nueva-funcionalidad
git push origin develop
```
✅ **Eliminar la rama `feature/*` si ya no es necesaria:**
```sh
git branch -d feature/nueva-funcionalidad
git push origin --delete feature/nueva-funcionalidad #elimina en el repositorio remoto
```

---



## 🚀 Crear y fusionar `developer` en `release`

**En la rama developer:**

✅  Realiza pruebas unitarias (testeo)

❌  Confirma que no haya errores ni conflictos en el código.

🪲 Si hay bugs o mejoras pendientes, corrígelos antes de pasar a release.

⚙️ Antes de mover el código a release, deben ejecutarse pruebas de integración para garantizar que las funcionalidades trabajadas en developer funcionan correctamente juntas.


Cuando `developer` esté estable y validada, se crea la rama `release` si no existe:
```sh
git checkout -b release
```

Si `release` ya existe, fusiona los cambios desde `developer`:
```sh
git checkout release
git merge developer
```

Sube los cambios al repositorio remoto:
```sh
git push origin release
```


---

## 🔍 Pruebas finales en `release`
En esta etapa, los testers revisan `release` en un entorno de pre-producción.
Si hay errores, se corrigen en `release` o en `developer` y se vuelve a fusionar.

---

