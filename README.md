# tutorial-de-git-y-giyhub-

taller 2

## 1.1 Acerca del control de versiones

* **Local:** guarda copias de versiones en tu propio equipo; es simple pero no permite colaborar.
* **Centralizado (CVCS):** un servidor único guarda todo (ej. Subversion); si falla, se pierde el historial.
* **Distribuido (DVCS):** cada persona clona el repositorio completo con todo su historial. Git pertenece a este grupo.

## 1.2 Una breve historia de Git

Git nació en 2005, cuando la comunidad del kernel de Linux dejó de usar BitKeeper y Linus Torvalds creó una herramienta propia. Sus metas: velocidad, diseño sencillo, soporte para ramas no lineales, totalmente distribuido y capaz de manejar proyectos grandes.

## 1.3 Fundamentos de Git

* Git guarda **instantáneas** (fotos del proyecto), no listas de diferencias.
* Casi todas las operaciones son **locales**, por eso son muy rápidas y funcionan sin conexión.
* Todo se verifica con una suma de comprobación **SHA-1**, lo que garantiza la integridad de los datos.
* Un archivo puede estar en tres estados: **modificado**, **preparado** (staged) o **confirmado** (committed).
* Tres áreas: directorio de trabajo, área de preparación y directorio de Git (el repositorio).

## 1.4 a 1.6 Instalación y primera configuración

Se trabaja desde la línea de comandos. Tras instalar Git, comprueba la versión y configura tu identidad, que quedará registrada en cada commit:

```bash
git --version
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
git config --list
```

## 1.7 ¿Cómo obtener ayuda?

```bash
git help <verbo>
git <verbo> --help
git add -h        # ayuda rápida
```

## Resumen

Ya sabes qué es el control de versiones, por qué Git es distribuido, cómo piensa (instantáneas, tres estados y tres áreas) y cómo instalarlo y configurar tu identidad.

Capítulo 2: Fundamentos de Git
> Este capítulo cubre lo esencial para trabajar a diario: crear o clonar repositorios, guardar cambios, ver el historial, deshacer errores y sincronizar con un remoto.
2.1 Obteniendo un repositorio
```bash
git init                      # convierte la carpeta actual en repositorio
git clone <url>                # copia un repositorio existente
```
2.2 Guardando cambios
Los archivos pasan por cuatro estados: sin seguimiento, sin modificar, modificado y preparado. El ciclo básico es:
```bash
git status                    # ver qué cambió
git add archivo.txt           # preparar el cambio
git commit -m "Mensaje"       # confirmarlo en el historial
git diff                      # cambios sin preparar
git diff --staged             # cambios ya preparados
```
Otras acciones de archivos
`.gitignore` lista los archivos que Git debe ignorar (logs, contraseñas, carpetas temporales).
`git rm` elimina un archivo y `git mv` lo renombra o lo mueve, dejando el cambio registrado.
2.3 Ver el historial
```bash
git log
git log --oneline --graph
git log -p -2                # muestra los 2 últimos con sus diferencias
```
2.4 Deshacer cosas
```bash
git commit --amend            # corrige el último commit
git restore --staged archivo  # saca un archivo del área de preparación
git restore archivo           # descarta cambios locales (¡no se recuperan!)
```
2.5 a 2.7 Remotos, etiquetas y alias
```bash
git remote -v                 # lista remotos
git remote add origin <url>   # vincula un remoto
git fetch origin              # descarga sin fusionar
git pull                      # descarga y fusiona
git push origin main          # sube tus commits
git tag -a v1.0 -m "Versión 1.0"
git config --global alias.st status
```
Resumen
Con estos comandos ya puedes crear un repositorio, registrar cambios, consultar el historial, corregir errores y compartir tu trabajo con GitHub.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

\---

*Fuente: Scott Chacon y Ben Straub,* [*Pro Git*](https://git-scm.com/book/es/v2)*, 2.ª edición (licencia CC BY-NC-SA 3.0).*

Capítulo 3: Ramificaciones en Git
> Las ramas permiten trabajar en una línea de desarrollo separada sin afectar el trabajo principal. En Git son muy baratas y rápidas, y es una de sus características más potentes.
3.1 ¿Qué es una rama?
Una rama es un apuntador móvil a un commit. HEAD señala la rama en la que estás trabajando; la rama inicial suele llamarse `main` (antes `master`).
3.2 Ramificar y fusionar
```bash
git branch nueva-rama         # crea la rama
git checkout -b nueva-rama    # crea y cambia (también: git switch -c)
git checkout main
git merge nueva-rama          # fusiona en la rama actual
```
Conflictos de fusión
Si dos ramas modifican la misma parte de un archivo, Git marca el conflicto con `<<<<<<<`, `=======` y `>>>>>>>`. Edita el archivo, deja la versión correcta, y luego ejecuta `git add` y `git commit` para cerrar la fusión.
3.3 Gestión de ramas
```bash
git branch -v                 # última confirmación de cada rama
git branch --merged           # ramas ya fusionadas
git branch -d nueva-rama      # borra una rama fusionada
```
3.4 Flujos de trabajo ramificados
Ramas de larga duración: por ejemplo `main` (estable) y `develop` (pruebas).
Ramas temáticas: cortas, para una sola funcionalidad o corrección; se fusionan y se borran.
3.5 y 3.6 Ramas remotas y rebase
Regla de oro: no hagas rebase de commits que ya publicaste y otras personas usan.
```bash
git push origin nueva-rama     # publica la rama
git push origin --delete nueva-rama
git rebase main               # reaplica tus commits sobre main
```
Resumen
Las ramas te dejan experimentar con seguridad. Aprendiste a crearlas, fusionarlas, resolver conflictos, gestionarlas y sincronizarlas con el remoto.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

Capítulo 4: Git en el Servidor
> Para colaborar necesitas un repositorio remoto accesible. Este capítulo explica los protocolos disponibles y cómo montar tu propio servidor o usar uno externo.
4.1 Los protocolos
Local: el remoto es otra carpeta del mismo equipo o de una red compartida.
HTTP: simple de abrir en cualquier red; el HTTP inteligente admite lectura y escritura.
SSH: el más usado para escribir; usa autenticación con claves.
Git: demonio de solo lectura, muy rápido pero sin autenticación.
4.2 Configurando Git en un servidor
En el servidor se usa un repositorio desnudo (bare), que solo contiene los datos de Git, sin archivos de trabajo:
```bash
git clone --bare mi_proyecto mi_proyecto.git
scp -r mi_proyecto.git usuario@servidor:/srv/git
```
4.3 y 4.4 Clave pública SSH y configuración
Cada colaborador genera su clave y entrega la parte pública para añadirla al archivo `authorized_keys` del usuario `git` en el servidor.
```bash
ssh-keygen -t ed25519 -C "tu-correo@ejemplo.com"
cat ~/.ssh/id_ed25519.pub
git init --bare proyecto.git      # en el servidor
```
4.5 a 4.9 Demonio, GitWeb, GitLab y alojamiento externo
git daemon` publica repositorios en solo lectura por el puerto 9418.
GitWeb ofrece una interfaz web sencilla para explorar repositorios.
GitLab es una plataforma completa que puedes instalar en tu servidor.
Los alojamientos externos (GitHub, GitLab.com, Bitbucket) evitan mantener infraestructura propia.
Resumen
Puedes alojar tus repositorios en tu propio servidor con SSH o usar un servicio externo. Para proyectos pequeños, un alojamiento externo es la opción más práctica.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

Capítulo 5: Git en Entornos Distribuidos
> Al ser distribuido, Git permite organizar el trabajo en equipo de muchas formas. Este capítulo presenta los flujos más comunes y cómo contribuir o mantener un proyecto.
5.1 Flujos de trabajo distribuidos
Centralizado: todos suben a un único repositorio compartido.
Gestor de integración: cada persona tiene su copia pública; una persona fusiona las contribuciones (el modelo de fork y pull request).
Dictador y tenientes: jerarquía para proyectos enormes, como el kernel de Linux.
5.2 Contribuyendo a un proyecto
Haz commits pequeños y con un solo propósito.
Comprueba espacios en blanco antes de confirmar con `git diff --check`.
Escribe buenos mensajes: una línea de resumen corta y, si hace falta, una explicación detallada.
En proyectos públicos: haz un fork, crea una rama temática, sube cambios y abre un pull request.
También se pueden enviar parches por correo con `git format-patch` y `git send-email`.
5.3 Manteniendo un proyecto
Quien mantiene un proyecto revisa y aplica contribuciones recibidas:
```bash
git apply parche.diff         # aplica un parche
git am parche.mbox            # aplica parches recibidos por correo
git cherry-pick <commit>      # trae un commit concreto
git describe main             # nombre legible para una versión
git shortlog                  # resumen de contribuciones
```
Resumen
Hay varios flujos de colaboración; el más popular en GitHub es el de fork y pull request. Commits claros y atómicos facilitan el trabajo de quien revisa.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

Capítulo 6: GitHub
> GitHub es la mayor plataforma de alojamiento de repositorios Git. Añade herramientas de colaboración como forks, pull requests, incidencias (issues) y organizaciones.
6.1 Creación y configuración de la cuenta
Crea tu cuenta gratuita en github.com y verifica tu correo.
Activa la autenticación en dos pasos para proteger tu cuenta.
Añade tu clave SSH o usa autenticación por navegador para hacer `push` sin escribir la contraseña.
6.2 Participando en proyectos
El flujo típico para contribuir a un proyecto ajeno es:
Fork: crea tu copia del repositorio en tu cuenta.
Clona tu fork y crea una rama temática.
Haz commits, súbelos a tu fork y abre un pull request.
Responde a los comentarios de la revisión; los nuevos commits se agregan al mismo PR.
```bash
git remote add upstream <url-del-original>
git fetch upstream
git merge upstream/main       # mantén tu fork actualizado
```
6.3 Mantenimiento de un proyecto
Crea el repositorio y añade colaboradores.
Gestiona pull requests: revisar, comentar, fusionar o cerrar.
Usa menciones (`@usuario`) y referencias a incidencias (`#12`).
Archivos útiles: `README.md`, `CONTRIBUTING.md` y `LICENSE`.
6.4 y 6.5 Organizaciones y scripting
Las organizaciones agrupan repositorios y personas en equipos con permisos. Para automatizar tareas, GitHub ofrece una API y webhooks que avisan a otros servicios cuando ocurre un evento.
Resumen
GitHub convierte Git en una plataforma de colaboración. Con fork, pull request y buena documentación puedes aportar a cualquier proyecto abierto o gestionar el tuyo.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

Capítulo 7: Herramientas de Git
> Más allá de commit y push, Git incluye herramientas avanzadas para seleccionar commits, reescribir la historia, buscar errores y manejar proyectos complejos.
7.1 a 7.3 Selección, organización interactiva y stash
Referencias relativas: `HEAD~2`, rangos `A..B` y `git reflog` para ver movimientos recientes.
`git add -p` permite preparar solo partes de un archivo.
`git stash` guarda cambios sin confirmar para retomarlos después.
```bash
git stash
git stash list
git stash pop                 # recupera y elimina el stash
git clean -n                   # simula la limpieza de archivos sin seguimiento
```
7.4 y 7.5 Firmar y buscar
Firma commits y etiquetas con GPG: `git commit -S`, `git tag -s`.
`git grep` busca texto en el proyecto y `git log -S "texto"` busca cuándo se añadió o quitó.
7.6 y 7.7 Reescribir la historia y reset
```bash
git rebase -i HEAD~3          # reordena, une o edita los 3 últimos commits
git reset --soft HEAD~1       # deshace el commit, conserva todo preparado
git reset --mixed HEAD~1      # deshace el commit, conserva archivos (por defecto)
git reset --hard HEAD~1       # descarta commit y cambios (peligroso)
```
7.8 a 7.14 Otras herramientas
Fusión avanzada y rerere: Git recuerda cómo resolviste un conflicto para reutilizarlo.
Depuración: `git blame` muestra quién cambió cada línea y `git bisect` encuentra el commit que introdujo un error.
Submódulos: incluyen otro repositorio dentro del tuyo (`git submodule add`).
Bundles empaquetan un repositorio en un archivo; replace sustituye objetos; el almacén de credenciales evita escribir la contraseña cada vez.
Resumen
Estas herramientas te dan control fino sobre la historia y la depuración. Úsalas con cuidado: reescribir la historia solo es seguro en commits que aún no has compartido.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

Capítulo 7: Herramientas de Git
> Más allá de commit y push, Git incluye herramientas avanzadas para seleccionar commits, reescribir la historia, buscar errores y manejar proyectos complejos.
7.1 a 7.3 Selección, organización interactiva y stash
Referencias relativas: `HEAD~2`, rangos `A..B` y `git reflog` para ver movimientos recientes.
`git add -p` permite preparar solo partes de un archivo.
`git stash` guarda cambios sin confirmar para retomarlos después.
```bash
git stash
git stash list
git stash pop                 # recupera y elimina el stash
git clean -n                   # simula la limpieza de archivos sin seguimiento
```
7.4 y 7.5 Firmar y buscar
Firma commits y etiquetas con GPG: `git commit -S`, `git tag -s`.
`git grep` busca texto en el proyecto y `git log -S "texto"` busca cuándo se añadió o quitó.
7.6 y 7.7 Reescribir la historia y reset
```bash
git rebase -i HEAD~3          # reordena, une o edita los 3 últimos commits
git reset --soft HEAD~1       # deshace el commit, conserva todo preparado
git reset --mixed HEAD~1      # deshace el commit, conserva archivos (por defecto)
git reset --hard HEAD~1       # descarta commit y cambios (peligroso)
```
7.8 a 7.14 Otras herramientas
Fusión avanzada y rerere: Git recuerda cómo resolviste un conflicto para reutilizarlo.
Depuración: `git blame` muestra quién cambió cada línea y `git bisect` encuentra el commit que introdujo un error.
Submódulos: incluyen otro repositorio dentro del tuyo (`git submodule add`).
Bundles empaquetan un repositorio en un archivo; replace sustituye objetos; el almacén de credenciales evita escribir la contraseña cada vez.
Resumen
Estas herramientas te dan control fino sobre la historia y la depuración. Úsalas con cuidado: reescribir la historia solo es seguro en commits que aún no has compartido.
---
Fuente: Scott Chacon y Ben Straub, Pro Git, 2.ª edición (licencia CC BY-NC-SA 3.0).

