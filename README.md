# buenasPracticas_git

Este readme permite constituir una guía de buenas prácticas a la hora de desarrollar un proyecto en equipo utilizando git.

Todo proyecto de desarrollo de software debe de tener como mínimo 4 ramas de desarrollo. 

**Rama Main/Master** 

Es la rama del proyecto en producción, y es la rama más delicada del proyecto, ya que toda acción 
sobre esta rama afecta directamente al cliente. 

**Rama Release**

Se crea a partir de develop cuando se prepara una nueva versión para producción.
Permite realizar pruebas y corregir errores antes de lanzar la versión final.
Se usa para estabilizar el código antes de que pase a la rama main o master.
Una vez que la versión está lista, los cambios se fusionan en main y también en develop (para asegurar que las correcciones no se pierdan en futuras versiones).

 **Rama Developer**
 
Es la rama donde se integran los cambios de las características en desarrollo.
Aquí se fusionan las ramas de funcionalidad (feature) una vez que los desarrolladores completan una nueva funcionalidad.
Puede considerarse una versión intermedia e inestable del software.
No se despliega en producción directamente.

**Rama Feature**

Son númerosas ramas que desarrollan un tarea en concreto. 
Cuando esa parte del código está implementada debe de fusionarse con la rama Developer.




![image](https://github.com/user-attachments/assets/4697b9a4-cb29-4fd9-b1c6-7aba6b414fd2)




⚠️ Advertencia: 

Siempre antes de hacer push (subir tus cambios a remoto), haz pull (descargas los cambios en remoto) y 
soluciona los conflictos en el caso de que los hubiera.


**FLUJO DE TRABAJO**

Desarrollo de nuevas funcionalidades en ramas feature/*.

Integración en develop cuando una funcionalidad está completa.

Creación de una release/* cuando se prepara una nueva versión.

Corrección de errores en la rama release, sin añadir nuevas características.

Fusión de release en main y etiquetado con un número de versión (v1.0.0, v1.1.0, etc.).

Fusión de release en develop para mantener las correcciones en futuras versiones.


 
**EJEMPLO PRÁCTICO**

Deseas añadir una nueva función a una aplicación que ha sido previamente desplegada en un servidor.

1️⃣ Crear la nueva rama feature basada en developer:

En primer lugar debemos desplazarnos a la rama developer con el comando checkout

```
git checkout developer
```

debemos hacer pull para actualizar los cambios que haya el repositorio remoto.

```
git pull origin developer
```

 cambiamos de rama y la creamos al mismo tiempo.

```
git checkout -b feature/nueva-funcionalidad
```

2️⃣ Trabajar en la funcionalidad y hacer commits en feature
```
git add .
git commit -m "Implementación de nueva funcionalidad"
```

3️⃣ Mantener la rama feature actualizada
En lugar de hacer un merge, es mejor hacer **rebase de developer en feature** para evitar commits innecesarios y mantener el historial limpio:

```
git checkout developer
git pull origin developer  # Asegurar que tienes la última versión
git checkout feature/nueva-funcionalidad
git rebase developer

```
4️⃣ Fusionar feature en developer cuando esté lista

```
git checkout developer
git merge feature/nueva-funcionalidad
git push origin developer
```
✅ Se recomienda eliminar la rama feature después del merge si ya no es necesaria:

```
git branch -d feature/nueva-funcionalidad

```

Si además existe en remoto:
```
git push origin --delete feature
```

**En la rama developer:**

✅  Realiza pruebas unitarias (testeo)

❌  Confirma que no haya errores ni conflictos en el código.

🪲 Si hay bugs o mejoras pendientes, corrígelos antes de pasar a release.

⚙️ Antes de mover el código a release, deben ejecutarse pruebas de integración para garantizar que las funcionalidades trabajadas en developer funcionan correctamente juntas.



## 🚀 Crear y fusionar developer en release
Cuando **developer** esté estable y validada, se crea la rama **release** si no existe:

```sh
git checkout -b release
```

Si la rama **release** ya existe y se está preparando una nueva versión, fusiona los cambios desde **developer**:

```sh
git checkout release
git merge developer
```

Luego, sube los cambios al repositorio remoto:

```sh
git push origin release
```

---

## 🔍 Realizar pruebas finales en release
En esta etapa, los testers revisan la rama **release** en un entorno de pre-producción. Aquí se busca detectar errores antes de la fusión en **main**.

Si se encuentran errores, pueden corregirse directamente en la rama **release**, o bien realizar los cambios en **developer** y luego volver a fusionarlos.














