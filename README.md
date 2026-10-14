# Tutorial de Git y GitHub

> Resumen práctico de los 10 capítulos del libro *Pro Git* (2.ª edición, en español), elaborado como parte de la **Actividad 2** del curso.

![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=flat&logo=markdown&logoColor=white)
![Licencia](https://img.shields.io/badge/licencia-CC%20BY--NC--SA%203.0-lightgrey)

## Descripción

Este repositorio reúne, en un solo lugar, un tutorial de Git y GitHub dividido por capítulos. Cada capítulo sigue la estructura del libro oficial *Pro Git* y resume sus ideas principales con explicaciones breves, comandos de ejemplo y un resumen final.

Está pensado para quien empieza desde cero y quiere entender **qué hace cada comando y por qué**, no solo copiarlo.

## Objetivos

- Entender qué es el control de versiones y por qué Git es el más utilizado.
- Dominar el ciclo básico de trabajo: `add`, `commit`, `push` y `pull`.
- Trabajar con ramas, fusiones y repositorios remotos.
- Colaborar en GitHub mediante forks y pull requests.
- Conocer herramientas avanzadas y el funcionamiento interno de Git.

## Contenido

| Capítulo | Tema | Qué aprenderás |
| :---: | --- | --- |
| 1 | [Inicio y control de versiones](#capítulo-1-inicio-y-control-de-versiones) | Conceptos base, historia e instalación |
| 2 | [Fundamentos de Git](#capítulo-2-fundamentos-de-git) | Crear repositorios, guardar cambios y sincronizar |
| 3 | [Ramificaciones en Git](#capítulo-3-ramificaciones-en-git) | Ramas, fusiones y rebase |
| 4 | [Git en el servidor](#capítulo-4-git-en-el-servidor) | Protocolos, SSH y alojamiento |
| 5 | [Git en entornos distribuidos](#capítulo-5-git-en-entornos-distribuidos) | Flujos de trabajo en equipo |
| 6 | [GitHub](#capítulo-6-github) | Cuentas, forks y pull requests |
| 7 | [Herramientas de Git](#capítulo-7-herramientas-de-git) | Stash, reset, búsqueda y depuración |
| 8 | [Personalización de Git](#capítulo-8-personalización-de-git) | Configuración, atributos y hooks |
| 9 | [Git y otros sistemas](#capítulo-9-git-y-otros-sistemas) | Convivir y migrar desde otros sistemas |
| 10 | [Los entresijos internos de Git](#capítulo-10-los-entresijos-internos-de-git) | Objetos, referencias y packfiles |

Además: [Guía rápida de comandos](#guía-rápida-de-comandos) · [Glosario](#glosario) · [Fuente y licencia](#fuente-y-licencia)

## Cómo usar este repositorio

Clona el repositorio y lee los capítulos en orden:

    git clone https://github.com/TU-USUARIO/tutorial-de-git-y-github.git
    cd tutorial-de-git-y-github

> [!TIP]
> Lo más efectivo es **practicar cada comando** en una carpeta de prueba mientras lees. Git se aprende haciendo.

---

## Capítulo 1: Inicio y control de versiones

> Un sistema de control de versiones registra los cambios de tus archivos a lo largo del tiempo, de modo que puedas volver a una versión anterior, comparar cambios y saber quién modificó qué.

### 1.1 Acerca del control de versiones

| Tipo | Cómo funciona | Limitación |
| --- | --- | --- |
| **Local** | Guarda copias de versiones en tu propio equipo | Simple, pero no permite colaborar |
| **Centralizado (CVCS)** | Un servidor único guarda todo (ej. Subversion) | Si el servidor falla, se pierde el historial |
| **Distribuido (DVCS)** | Cada persona clona el repositorio completo con todo su historial | Git pertenece a este grupo |

### 1.2 Una breve historia de Git

Git nació en 2005, cuando la comunidad del kernel de Linux dejó de usar BitKeeper y Linus Torvalds creó una herramienta propia. Sus metas fueron:

- Velocidad.
- Diseño sencillo.
- Soporte para ramas no lineales.
- Ser totalmente distribuido.
- Capacidad para manejar proyectos grandes.

### 1.3 Fundamentos de Git

- Git guarda **instantáneas** (fotos del proyecto), no listas de diferencias.
- Casi todas las operaciones son **locales**, por eso son muy rápidas y funcionan sin conexión.
- Todo se verifica con una suma de comprobación **SHA-1**, lo que garantiza la integridad de los datos.
- Un archivo puede estar en tres estados:

| Estado | Significado | Cómo se llega a él |
| --- | --- | --- |
| **Modificado** | Cambiaste el archivo, pero aún no lo guardas | Editar el archivo |
| **Preparado** (*staged*) | Marcaste el cambio para el próximo commit | `git add` |
| **Confirmado** (*committed*) | El cambio ya está en el historial | `git commit` |

Esos estados corresponden a tres áreas: el **directorio de trabajo**, el **área de preparación** y el **directorio de Git** (el repositorio).

### 1.4 a 1.6 Instalación y primera configuración

Se trabaja desde la línea de comandos. Tras instalar Git, comprueba la versión y configura tu identidad, que quedará registrada en cada commit:

    git --version
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu-correo@ejemplo.com"
    git config --list

### 1.7 ¿Cómo obtener ayuda?

Git incluye su propio manual:

    git help <verbo>
    git <verbo> --help
    git add -h        # ayuda rápida

### Resumen del capítulo 1

> Ya sabes qué es el control de versiones, por qué Git es distribuido, cómo piensa (instantáneas, tres estados y tres áreas) y cómo instalarlo y configurar tu identidad.

[↑ Volver al índice](#contenido)

---

## Capítulo 2: Fundamentos de Git

> Este capítulo cubre lo esencial para trabajar a diario: crear o clonar repositorios, guardar cambios, ver el historial, deshacer errores y sincronizar con un remoto.

### 2.1 Obteniendo un repositorio

Puedes crear uno nuevo o copiar uno existente:

    git init                       # convierte la carpeta actual en repositorio
    git clone <url>                # copia un repositorio existente

### 2.2 Guardando cambios

Los archivos pasan por cuatro estados: sin seguimiento, sin modificar, modificado y preparado. El ciclo básico es:

    git status                     # ver qué cambió
    git add archivo.txt            # preparar el cambio
    git commit -m "Mensaje"        # confirmarlo en el historial
    git diff                       # cambios sin preparar
    git diff --staged              # cambios ya preparados

**Otras acciones de archivos**

- `.gitignore` lista los archivos que Git debe ignorar (logs, contraseñas, carpetas temporales).
- `git rm` elimina un archivo y `git mv` lo renombra o lo mueve, dejando el cambio registrado.

> [!TIP]
> Escribe mensajes de commit claros: explican **qué** cambió y facilitan encontrar errores después.

### 2.3 Ver el historial de confirmaciones

    git log
    git log --oneline --graph
    git log -p -2                  # muestra los 2 últimos con sus diferencias

### 2.4 Deshacer cosas

    git commit --amend             # corrige el último commit
    git restore --staged archivo   # saca un archivo del área de preparación
    git restore archivo            # descarta cambios locales

> [!WARNING]
> `git restore archivo` descarta los cambios locales y **no se pueden recuperar**.

### 2.5 a 2.7 Remotos, etiquetas y alias

Con un remoto sincronizas tu trabajo con GitHub; las etiquetas marcan versiones; los alias acortan comandos:

    git remote -v                  # lista remotos
    git remote add origin <url>    # vincula un remoto
    git fetch origin               # descarga sin fusionar
    git pull                       # descarga y fusiona
    git push origin main           # sube tus commits
    git tag -a v1.0 -m "Versión 1.0"
    git config --global alias.st status

### Resumen del capítulo 2

> Con estos comandos ya puedes crear un repositorio, registrar cambios, consultar el historial, corregir errores y compartir tu trabajo con GitHub.

[↑ Volver al índice](#contenido)

---

## Capítulo 3: Ramificaciones en Git

> Las ramas permiten trabajar en una línea de desarrollo separada sin afectar el trabajo principal. En Git son muy baratas y rápidas, y es una de sus características más potentes.

### 3.1 ¿Qué es una rama?

Una rama es un apuntador móvil a un commit. **HEAD** señala la rama en la que estás trabajando; la rama inicial suele llamarse `main` (antes `master`).

### 3.2 Procedimientos básicos para ramificar y fusionar

    git branch nueva-rama          # crea la rama
    git checkout -b nueva-rama     # crea y cambia (también: git switch -c)
    git checkout main
    git merge nueva-rama           # fusiona en la rama actual

**Conflictos de fusión.** Si dos ramas modifican la misma parte de un archivo, Git marca el conflicto con `<<<<<<<`, `=======` y `>>>>>>>`. Edita el archivo, deja la versión correcta y luego ejecuta `git add` y `git commit` para cerrar la fusión.

### 3.3 Gestión de ramas

    git branch -v                  # última confirmación de cada rama
    git branch --merged            # ramas ya fusionadas
    git branch -d nueva-rama       # borra una rama fusionada

### 3.4 Flujos de trabajo ramificados

- **Ramas de larga duración:** por ejemplo `main` (estable) y `develop` (pruebas).
- **Ramas temáticas:** cortas, para una sola funcionalidad o corrección; se fusionan y se borran.

### 3.5 y 3.6 Ramas remotas y reorganización del trabajo

Publica, borra y reorganiza ramas con:

    git push origin nueva-rama     # publica la rama
    git push origin --delete nueva-rama
    git rebase main                # reaplica tus commits sobre main

> [!WARNING]
> Regla de oro: **no hagas rebase de commits que ya publicaste** y que otras personas usan.

### Resumen del capítulo 3

> Las ramas te dejan experimentar con seguridad. Aprendiste a crearlas, fusionarlas, resolver conflictos, gestionarlas y sincronizarlas con el remoto.

[↑ Volver al índice](#contenido)

---

## Capítulo 4: Git en el servidor

> Para colaborar necesitas un repositorio remoto accesible. Este capítulo explica los protocolos disponibles y cómo montar tu propio servidor o usar uno externo.

### 4.1 Los protocolos

| Protocolo | Característica |
| --- | --- |
| **Local** | El remoto es otra carpeta del mismo equipo o de una red compartida |
| **HTTP** | Simple de abrir en cualquier red; el HTTP inteligente admite lectura y escritura |
| **SSH** | El más usado para escribir; usa autenticación con claves |
| **Git** | Demonio de solo lectura, muy rápido pero sin autenticación |

### 4.2 Configurando Git en un servidor

En el servidor se usa un repositorio **desnudo** (*bare*), que solo contiene los datos de Git, sin archivos de trabajo:

    git clone --bare mi_proyecto mi_proyecto.git
    scp -r mi_proyecto.git usuario@servidor:/srv/git

### 4.3 y 4.4 Clave pública SSH y configuración del servidor

Cada colaborador genera su clave y entrega la parte pública para añadirla al archivo `authorized_keys` del usuario `git` en el servidor:

    ssh-keygen -t ed25519 -C "tu-correo@ejemplo.com"
    cat ~/.ssh/id_ed25519.pub
    git init --bare proyecto.git       # en el servidor

### 4.5 a 4.9 Demonio, GitWeb, GitLab y alojamiento externo

- `git daemon` publica repositorios en solo lectura por el puerto 9418.
- **GitWeb** ofrece una interfaz web sencilla para explorar repositorios.
- **GitLab** es una plataforma completa que puedes instalar en tu servidor.
- Los **alojamientos externos** (GitHub, GitLab.com, Bitbucket) evitan mantener infraestructura propia.

### Resumen del capítulo 4

> Puedes alojar tus repositorios en tu propio servidor con SSH o usar un servicio externo. Para proyectos pequeños, un alojamiento externo es la opción más práctica.

[↑ Volver al índice](#contenido)

---

## Capítulo 5: Git en entornos distribuidos

> Al ser distribuido, Git permite organizar el trabajo en equipo de muchas formas. Este capítulo presenta los flujos más comunes y cómo contribuir o mantener un proyecto.

### 5.1 Flujos de trabajo distribuidos

| Flujo | Descripción |
| --- | --- |
| **Centralizado** | Todos suben a un único repositorio compartido |
| **Gestor de integración** | Cada persona tiene su copia pública y una persona fusiona las contribuciones (modelo de fork y pull request) |
| **Dictador y tenientes** | Jerarquía para proyectos enormes, como el kernel de Linux |

### 5.2 Contribuyendo a un proyecto

- Haz commits **pequeños y con un solo propósito**.
- Comprueba espacios en blanco antes de confirmar con `git diff --check`.
- Escribe buenos mensajes: una línea de resumen corta y, si hace falta, una explicación detallada.
- En proyectos públicos: haz un **fork**, crea una rama temática, sube cambios y abre un pull request.
- También se pueden enviar parches por correo con `git format-patch` y `git send-email`.

### 5.3 Manteniendo un proyecto

Quien mantiene un proyecto revisa y aplica las contribuciones recibidas:

    git apply parche.diff          # aplica un parche
    git am parche.mbox             # aplica parches recibidos por correo
    git cherry-pick <commit>       # trae un commit concreto
    git describe main              # nombre legible para una versión
    git shortlog                   # resumen de contribuciones

### Resumen del capítulo 5

> Hay varios flujos de colaboración; el más popular en GitHub es el de fork y pull request. Commits claros y atómicos facilitan el trabajo de quien revisa.

[↑ Volver al índice](#contenido)

---

## Capítulo 6: GitHub

> GitHub es la mayor plataforma de alojamiento de repositorios Git. Añade herramientas de colaboración como forks, pull requests, incidencias (*issues*) y organizaciones.

### 6.1 Creación y configuración de la cuenta

- Crea tu cuenta gratuita en [github.com](https://github.com) y verifica tu correo.
- Activa la **autenticación en dos pasos** para proteger tu cuenta.
- Añade tu clave SSH o usa autenticación por navegador para hacer `push` sin escribir la contraseña.

### 6.2 Participando en proyectos

El flujo típico para contribuir a un proyecto ajeno es:

1. **Fork:** crea tu copia del repositorio en tu cuenta.
2. Clona tu fork y crea una rama temática.
3. Haz commits, súbelos a tu fork y abre un **pull request**.
4. Responde a los comentarios de la revisión; los nuevos commits se agregan al mismo PR.

Para mantener tu fork actualizado respecto al original:

    git remote add upstream <url-del-original>
    git fetch upstream
    git merge upstream/main        # mantén tu fork actualizado

### 6.3 Mantenimiento de un proyecto

- Crea el repositorio y añade **colaboradores**.
- Gestiona pull requests: revisar, comentar, fusionar o cerrar.
- Usa menciones (`@usuario`) y referencias a incidencias (`#12`).
- Archivos útiles: `README.md`, `CONTRIBUTING.md` y `LICENSE`.

### 6.4 y 6.5 Organizaciones y scripting

Las **organizaciones** agrupan repositorios y personas en equipos con permisos. Para automatizar tareas, GitHub ofrece una **API** y **webhooks** que avisan a otros servicios cuando ocurre un evento.

### Resumen del capítulo 6

> GitHub convierte Git en una plataforma de colaboración. Con fork, pull request y buena documentación puedes aportar a cualquier proyecto abierto o gestionar el tuyo.

[↑ Volver al índice](#contenido)

---

## Capítulo 7: Herramientas de Git

> Más allá de commit y push, Git incluye herramientas avanzadas para seleccionar commits, reescribir la historia, buscar errores y manejar proyectos complejos.

### 7.1 a 7.3 Selección, organización interactiva y stash

- Referencias relativas: `HEAD~2`, rangos `A..B` y `git reflog` para ver movimientos recientes.
- `git add -p` permite preparar solo partes de un archivo.
- `git stash` guarda cambios sin confirmar para retomarlos después.

Comandos de ejemplo:

    git stash
    git stash list
    git stash pop                  # recupera y elimina el stash
    git clean -n                   # simula la limpieza de archivos sin seguimiento

### 7.4 y 7.5 Firmar y buscar

- Firma commits y etiquetas con GPG: `git commit -S`, `git tag -s`.
- `git grep` busca texto en el proyecto y `git log -S "texto"` busca cuándo se añadió o quitó.

### 7.6 y 7.7 Reescribir la historia y reset

    git rebase -i HEAD~3           # reordena, une o edita los 3 últimos commits
    git reset --soft HEAD~1        # deshace el commit, conserva todo preparado
    git reset --mixed HEAD~1       # deshace el commit, conserva archivos (por defecto)
    git reset --hard HEAD~1        # descarta commit y cambios

> [!WARNING]
> `git reset --hard` es peligroso: descarta el commit y los cambios de forma irreversible.

### 7.8 a 7.14 Otras herramientas

- **Fusión avanzada y rerere:** Git recuerda cómo resolviste un conflicto para reutilizarlo.
- **Depuración:** `git blame` muestra quién cambió cada línea y `git bisect` encuentra el commit que introdujo un error.
- **Submódulos:** incluyen otro repositorio dentro del tuyo (`git submodule add`).
- **Bundles** empaquetan un repositorio en un archivo; **replace** sustituye objetos; el **almacén de credenciales** evita escribir la contraseña cada vez.

### Resumen del capítulo 7

> Estas herramientas te dan control fino sobre la historia y la depuración. Úsalas con cuidado: reescribir la historia solo es seguro en commits que aún no has compartido.

[↑ Volver al índice](#contenido)

---

## Capítulo 8: Personalización de Git

> Git es muy configurable: puedes ajustar su comportamiento, definir reglas para tus archivos y automatizar acciones con ganchos (*hooks*).

### 8.1 Configuración de Git

La configuración tiene tres niveles: `--system` (todo el equipo), `--global` (tu usuario) y `--local` (solo el repositorio). Algunos ajustes útiles:

    git config --global core.editor "code --wait"
    git config --global commit.template ~/.gitmessage
    git config --global core.autocrlf true     # saltos de línea en Windows
    git config --global color.ui auto
    git config --global help.autocorrect 10    # corrige comandos mal escritos

### 8.2 Git Attributes

El archivo `.gitattributes` define cómo trata Git ciertos archivos. Sirve, por ejemplo, para:

- Marcar archivos como **binarios** o definir cómo compararlos.
- Excluir archivos al exportar el proyecto (`export-ignore`).
- Elegir estrategias de fusión para archivos concretos.

### 8.3 Puntos de enganche (hooks)

Los hooks son scripts que Git ejecuta ante ciertos eventos. Viven en la carpeta `.git/hooks`.

- **Del lado del cliente:** `pre-commit` (revisar antes de confirmar), `prepare-commit-msg`, `commit-msg` (validar el mensaje) y `post-commit`.
- **Del lado del servidor:** `pre-receive`, `update` y `post-receive`, útiles para imponer reglas al recibir un push.

### 8.4 Ejemplo de política

Con un hook en el servidor se puede exigir un formato en los mensajes de commit, restringir quién modifica ciertas carpetas o rechazar pushes que no sean avances rápidos (*fast-forward*).

### Resumen del capítulo 8

> Personalizar Git te ayuda a trabajar más cómodo y a mantener estándares de calidad automáticamente mediante atributos y hooks.

[↑ Volver al índice](#contenido)

---

## Capítulo 9: Git y otros sistemas

> No siempre se parte desde cero: muchos proyectos viven en otros sistemas de control de versiones. Git puede interactuar con ellos y también importar su historia.

### 9.1 Git como cliente

Puedes usar Git como cliente de otros sistemas y conservar sus ventajas (ramas locales, commits sin conexión):

- **Subversion:** con `git svn`.
- **Mercurial:** mediante puentes como `git-remote-hg`.
- **Perforce:** con `git p4`.

Ejemplo con Subversion:

    git svn clone <url-del-repositorio-svn>
    git svn dcommit                # envía tus commits al servidor Subversion
    git svn rebase                 # trae los cambios nuevos

### 9.2 Migración a Git

Para abandonar el sistema anterior y pasar todo a Git:

- Con Subversion, Mercurial o Perforce se usan herramientas de importación que convierten el historial en commits de Git.
- Para sistemas poco comunes se puede escribir un **importador propio** con `git fast-import`.
- Después de migrar, verifica ramas, etiquetas y autores (se suele mapear usuarios a nombres y correos).

### Resumen del capítulo 9

> Git convive con otros sistemas: puedes usarlo como cliente mientras la organización migra, o importar todo el historial para empezar de lleno con Git.

[↑ Volver al índice](#contenido)

---

## Capítulo 10: Los entresijos internos de Git

> Entender cómo funciona Git por dentro ayuda a usarlo mejor. Git es, en el fondo, un sistema de archivos direccionable por contenido con una interfaz de control de versiones encima.

### 10.1 Fontanería y porcelana

Los comandos de **fontanería** (*plumbing*) son de bajo nivel; los de **porcelana** (`add`, `commit`, `push`...) son los que usamos a diario y se apoyan en los primeros.

### 10.2 Los objetos de Git

Todo se guarda en `.git/objects`, identificado por su suma SHA-1. Hay cuatro tipos de objeto:

| Objeto | Qué guarda |
| --- | --- |
| **blob** | El contenido de un archivo |
| **tree** | Un directorio, que apunta a blobs y otros trees |
| **commit** | Apunta a un tree y a sus padres, y guarda autor y mensaje |
| **tag** | Una etiqueta anotada |

Para explorarlos directamente:

    echo "hola" | git hash-object -w --stdin
    git cat-file -p <sha1>         # muestra el contenido
    git cat-file -t <sha1>         # muestra el tipo

### 10.3 a 10.5 Referencias, packfiles y refspec

- Las **referencias** son archivos en `.git/refs` que guardan un SHA-1 con un nombre legible (ramas, etiquetas); `HEAD` apunta a la rama actual.
- Los **packfiles** comprimen muchos objetos en uno solo; `git gc` los genera.
- Un **refspec** define cómo se mapean referencias remotas y locales, por ejemplo `+refs/heads/*:refs/remotes/origin/*`.

### 10.6 a 10.8 Transferencia, mantenimiento y entorno

- Protocolos de transferencia: el **tonto** (HTTP simple) y el **inteligente** (negocia qué objetos enviar).
- `git gc` optimiza el repositorio, `git fsck` revisa su integridad y permite recuperar datos perdidos.
- Variables de entorno como `GIT_DIR`, `GIT_AUTHOR_NAME` o `GIT_TRACE` modifican o depuran el comportamiento de Git.

### Resumen del capítulo 10

> Git guarda contenido en objetos, enlazados por referencias. Conocer esta base te permite entender mejor lo que ocurre tras cada comando y recuperar información cuando algo sale mal.

[↑ Volver al índice](#contenido)

---

## Guía rápida de comandos

| Comando | Para qué sirve |
| --- | --- |
| `git init` | Crea un repositorio nuevo |
| `git clone <url>` | Copia un repositorio remoto |
| `git status` | Muestra el estado de los archivos |
| `git add <archivo>` | Prepara cambios para el commit |
| `git commit -m "mensaje"` | Guarda los cambios en el historial |
| `git log --oneline` | Muestra el historial resumido |
| `git diff` | Muestra las diferencias sin confirmar |
| `git branch` | Lista o crea ramas |
| `git checkout -b <rama>` | Crea una rama y se cambia a ella |
| `git merge <rama>` | Fusiona una rama en la actual |
| `git remote add origin <url>` | Vincula el repositorio con GitHub |
| `git push origin <rama>` | Sube los commits a GitHub |
| `git pull` | Descarga y fusiona cambios del remoto |
| `git stash` | Guarda cambios sin confirmar temporalmente |

## Glosario

| Término | Definición |
| --- | --- |
| **Repositorio** | Carpeta de proyecto con todo su historial de cambios |
| **Commit** | Instantánea del proyecto guardada en el historial |
| **Rama (branch)** | Línea de desarrollo independiente |
| **HEAD** | Apuntador a la rama o commit en el que estás |
| **Remoto (remote)** | Versión del repositorio alojada en otro lugar, como GitHub |
| **Fork** | Copia personal de un repositorio ajeno en tu cuenta |
| **Pull request** | Solicitud para que tus cambios sean revisados y fusionados |
| **Staging** | Área donde se preparan los cambios antes del commit |
| **Merge** | Unión de los cambios de dos ramas |
| **Conflicto** | Situación en que Git no puede fusionar solo y necesita tu decisión |

## Fuente y licencia

Contenido elaborado a partir de Scott Chacon y Ben Straub, [*Pro Git*](https://git-scm.com/book/es/v2), 2.ª edición, publicado bajo la licencia [Creative Commons Reconocimiento-NoComercial-CompartirIgual 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/). Este resumen mantiene la misma licencia.

## Autor

**Tu Nombre**
- GitHub: [@TU-USUARIO](https://github.com/TU-USUARIO)
- Curso: _Nombre del curso_ · Actividad 2