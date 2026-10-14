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

\---

*Fuente: Scott Chacon y Ben Straub,* [*Pro Git*](https://git-scm.com/book/es/v2)*, 2.ª edición (licencia CC BY-NC-SA 3.0).*



