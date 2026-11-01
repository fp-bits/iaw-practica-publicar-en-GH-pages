![Github Pages](https://cdn-wcsm.alura.com.br/2025/04/imagen4.png "Github Pages")

# Práctica-Examen de nuestro primer despliegue en la Web
## Publicar tu sitio Hugo con GitHub Pages

**Módulo:** Implantación de Aplicaciones Web (IAW) — 2º ASIR
**Previas requeridas:** [P1.1 — Tu perfil de GitHub](https://librebits.info/2asir/iaw/perfil-github-readme-html-css/) y [P1.2 — Tu mini sitio web de la mano de Hugo](https://librebits.info/2asir/iaw/mini-sitio-web-con-hugo/)

Comienza el examen práctico del módulo. El reto consiste en **publicar en Internet, a través de [GitHub Pages](https://docs.github.com/es/pages), el mini sitio Hugo que construiste en P1.2**. Esta práctica-examen la puedes empezar desde ahora mismo, si quieres. De este modo el día señalado bastará con depurarla.

El día del examen práctico te propondré una serie de mejoras y cambios en ese mismo proyecto, que deberás implementar durante el tiempo establecido.

*Fecha* de la práctica-examen: **[A CONFIRMAR POR EL PROFESOR]**
*Hora* de la práctica-examen: **[A CONFIRMAR POR EL PROFESOR]**

> 💡 **Idea clave:** Hugo es un *generador de sitios estáticos*. Tú escribes **fuente** (`content/`, `layouts/`, `hugo.toml`…) y Hugo **genera HTML plano**. GitHub Pages solo sirve ese HTML plano. Todo el flujo de la práctica es: *editar → construir → commit → push → comprobar*.

---

## Tabla de contenido (TOC)

- [0. Flujo de trabajo (visión general)](#0-flujo-de-trabajo-visión-general)
- [1. Punto de partida: tu sitio Hugo de P1.2](#1-punto-de-partida-tu-sitio-hugo-de-p12)
- [2. Crea el repositorio en GitHub y sube el código](#2-crea-el-repositorio-en-github-y-sube-el-código)
- [3. Configura Hugo para GitHub Pages](#3-configura-hugo-para-github-pages)
- [4. Construye el sitio](#4-construye-el-sitio)
- [5. Haz un commit y sube los cambios](#5-haz-un-commit-y-sube-los-cambios)
- [6. Configura GitHub Pages](#6-configura-github-pages)
- [7. Visualiza tu web](#7-visualiza-tu-web)
- [8. Personaliza el título y la descripción](#8-personaliza-el-título-y-la-descripción)
- [Problemas típicos](#problemas-típicos)
- [Entregable](#entregable)
- [Evaluación](#evaluación)
- [Recursos adicionales](#recursos-adicionales)

---

### 0. Flujo de trabajo (visión general)

```
 editar (content/, layouts/, hugo.toml)
        │
        ▼
 hugo server -D      ← probar en local (http://localhost:1313/)
        │
        ▼
 hugo                ← construir: genera docs/ (HTML plano, sin borradores)
        │
        ▼
 git add . && git commit && git push
        │
        ▼
 GitHub Pages sirve main:/docs  →  https://TU-USUARIO.github.io/TU-REPO/
```

Regla de oro: **lo que ves en `hugo server -D` no es lo que se publica**; se publica lo que hay en `docs/` *después* de ejecutar `hugo` y hacer `push`.

### 1. Punto de partida: tu sitio Hugo de P1.2

- Localiza en tu VM la carpeta de tu mini sitio (la creada con `hugo new site MI-SITIO`).
- Comprueba que funciona en local, con tu parcial, tus páginas de contenido, el blog y el enlace a tu perfil de GitHub:
  ```bash
  cd MI-SITIO
  hugo version
  hugo server -D
  ```
  Abre <http://localhost:1313/> y revisa que todo se ve bien **antes** de publicar.
- Si tu sitio de P1.2 quedó con el texto de prueba en la portada o sin un parcial real (fichero en `layouts/partials/` incluido con `{{ partial "x.html" . }}`), corrígelo ahora.

### 2. Crea el repositorio en GitHub y sube el código

- En GitHub crea un repositorio **vacío** (sin README ni licencia) en tu cuenta, por ejemplo `mini-sitio-hugo`.
  - Para URL pública gratuita el repositorio debe ser **público**.
- Desde la terminal, dentro de la carpeta de tu sitio:
  ```bash
  git init -b main                      # omite si ya es un repo
  git add .
  git commit -m "Mini sitio Hugo de P1.2"
  git remote add origin https://github.com/TU-USUARIO/mini-sitio-hugo.git
  git push -u origin main
  ```
- Trabaja con `git` **desde la terminal** y haz **varios commits** a medida que avanzas (no uno único al final): se nota, y se valora.

### 3. Configura Hugo para GitHub Pages

GitHub Pages sirve tu sitio bajo una subruta (`/TU-REPO/`) y, con el modo «Deploy from a branch», solo puede servir la raíz del repo o la carpeta `/docs`. Hay que decírselo a Hugo en `hugo.toml`:

```toml
baseURL = "https://TU-USUARIO.github.io/mini-sitio-hugo/"
languageCode = "es"
title = "Mi sitio web práctico"
publishDir = "docs"          # Hugo escribe aquí el HTML generado
```

Además, crea un fichero vacío para que GitHub **no** procese tu `docs/` con Jekyll (sirve el HTML tal cual):

```bash
mkdir -p static && touch static/.nojekyll      # Hugo lo copiará a docs/.nojekyll
```

> ⚠️ **Enlaces y CSS bajo subruta:** no escribas rutas absolutas a mano como `href="/css/estilo.css"` en tus plantillas (apuntarían a `tuusuario.github.io/css/…`, no a tu repo). Usa las funciones de Hugo: `{{ "css/estilo.css" | relURL }}` o `{{ .Site.Home.RelPermalink }}`. Ver [relURL](https://gohugo.io/functions/urls/relurl/).

### 4. Construye el sitio

```bash
hugo                 # genera docs/ a partir de tu código fuente
ls docs              # debe haber index.html, .nojekyll, tu blog, etc.
```

- `hugo server -D` **incluye** los borradores (`draft: true`); `hugo` **no**. Si una página tuya tiene `draft: true`, no aparecerá en el sitio publicado: cámbiala a `draft: false` antes de construir.
- Si cambias o borras contenido, usa `hugo --cleanDestinationDir` para eliminar de `docs/` ficheros que ya no existen.
- Puedes abrir `docs/index.html` en el navegador como comprobación rápida, pero la prueba real es la URL de GitHub Pages (paso 7).

### 5. Haz un commit y sube los cambios

El HTML generado **forma parte del repositorio** (es lo que GitHub va a servir). Guarda y sube todo:

```bash
git status
git add .
git commit -m "Configurado baseURL y generado docs/ para GitHub Pages"
git push
```

### 6. Configura GitHub Pages

- Ve a la pestaña **Settings** de tu repositorio (`TU-USUARIO/mini-sitio-hugo`).
- En el menú lateral, busca la sección **Pages**.
- En **Build and deployment → Source**, selecciona **Deploy from a branch**.
- En **Branch** elige `main` y la carpeta **`/docs`** (no `/ (root)`).
- Pulsa **Save**.

### 7. Visualiza tu web

- GitHub publicará el sitio en la URL:
  `https://TU-USUARIO.github.io/mini-sitio-hugo/`
  *(Cambia `TU-USUARIO` por tu nombre de usuario en GitHub y el nombre del repo por el tuyo)*
- Espera uno o dos minutos: puedes seguir el despliegue en la pestaña **Actions** (workflow «pages build and deployment»).
- Comprueba, **en la URL pública**: portada con tu contenido (no el texto de prueba), parcial visible, segunda página, blog con al menos una entrada y el enlace a tu perfil de GitHub.

### 8. Personaliza el título y la descripción

Con Hugo la configuración vive en `hugo.toml` (el equivalente al `_config.yml` de Jekyll). Añade o edita:

```toml
title = "Mi sitio web práctico"

[params]
  description = "Ejercicio de publicación con Hugo y GitHub Pages"
```

Y úsalo en tu plantilla/parcial de cabecera:

```go-html-template
<title>{{ .Site.Title }}</title>
<meta name="description" content="{{ .Site.Params.description }}">
```

Haz `hugo`, commit y push de los cambios (código fuente **y** `docs/`).

### Problemas típicos

| Síntoma | Causa probable | Solución |
|:---|:---|:---|
| 404 en la URL de Pages | Pages apunta a `/ (root)` en vez de `/docs`, o `docs/` no está subido | Revisa paso 6; `git ls-files docs \| head` |
| La web sale sin estilos | `baseURL` incorrecto o rutas absolutas `/css/…` | Revisa `baseURL` y usa `relURL` (paso 3) |
| Falta una página o una entrada del blog | `draft: true` | Ponlo a `false` y vuelve a ejecutar `hugo` |
| Cambio visible en local pero no en la web | Olvidaste `hugo` + `git push` | Repite pasos 4 y 5 |
| La portada muestra «Hola mundo» | Texto de prueba en `layouts/index.html` o `home.html` | Sustitúyelo por tu contenido (ver P1.2) |
| Ves tu `README.md` en vez de la web | Pages sirve `/ (root)` sin `index.html` | Cambia a `/docs` |

### Entregable

1. URL pública de tu sitio en GitHub Pages (`https://TU-USUARIO.github.io/…`).
2. URL de tu repositorio GitHub (con `docs/` y el código fuente Hugo).
3. Captura de **Settings → Pages** mostrando `main` + `/docs` y el sitio publicado.

Entrega por el medio indicado en clase (o vía [servidor sFTP](https://librebits.info/blog/2asir-conexion-sftp-como-subir-tus-entregas/)).

> 💻 **Sobre el repositorio Git:** varios commits con mensajes descriptivos y marcas de tiempo distintas, trabajando con `git` desde la terminal. Es parte de la evaluación.

### Evaluación

Consulta la [RÚBRICA DE CALIFICACIÓN](RUBRICA-de-CALIFICACION.md) para saber qué se valora y cómo se reparten los 10 puntos.

### Recursos adicionales

- [Hugo — Host on GitHub Pages](https://gohugo.io/host-and-deploy/host-on-github-pages/) (la guía oficial usa GitHub Actions: una ampliación posible)
- [Hugo — Configuración (`baseURL`, `publishDir`)](https://gohugo.io/configuration/all/)
- [Hugo — `relURL`](https://gohugo.io/functions/urls/relurl/)
- [Hugo Codex — Empezando (español)](https://hugocodex.org/es/empezando/)
- [Guía oficial de GitHub Pages (español)](https://docs.github.com/es/pages)
- [Configurar una fuente de publicación para GitHub Pages](https://docs.github.com/es/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Paso a Paso para activar tu proyecto en GitHub Pages — Alura Latam](https://www.aluracursos.com/blog/github-pages)

"Recuerda ... KISS!" :-)
