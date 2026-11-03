# RUBRICA DE CALIFICACIÓN — PrácticaX2:  publicar tu sitio Hugo en GitHub Pages

**Módulo:** Implantación de Aplicaciones Web (IAW) — 2º ASIR
**Enunciado:** [README.md](README.md) · **Previas:** P1.1 (perfil GitHub), P1.2 (mini sitio Hugo)

## Índice

- [Criterios de contenido (10 puntos)](#criterios-de-contenido-10-puntos)
- [Convención en vivo vs. online, con matiz de `git log`](#convención-en-vivo-vs-online-con-matiz-de-git-log)
- [Escala orientativa](#escala-orientativa)
- [Lista de comprobación rápida para el profesor](#lista-de-comprobación-rápida-para-el-profesor)
- [Plantilla de feedback](#plantilla-de-feedback)

---

## Criterios de contenido (10 puntos)

### Implementación técnica — 7 puntos

| **Criterio** | **Peso** | **Qué se valora** |
|:---|:---:|:---|
| **Repositorio con el código fuente Hugo** | 1p | Repo público en GitHub con `content/`, `layouts/` (incluido el parcial real), `hugo.toml`…; subido con `git` |
| **Configuración de Hugo para Pages** | 1.5p | `baseURL` correcto (`https://USUARIO.github.io/REPO/`), `publishDir = "docs"`, `title` personalizado; `static/.nojekyll` presente |
| **Construcción y `docs/` en el repo** | 1p | `docs/` generado con `hugo` y **commiteado**; sin borradores perdidos (`draft: false`); `docs/` coherente con el código fuente |
| **GitHub Pages configurado** | 1p | Settings → Pages: *Deploy from a branch*, `main` + `/docs` (verificable por captura o en el repo) |
| **Sitio publicado y accesible** | 2p | La URL pública responde, sin 404, **sin CSS/enlaces rotos** (rutas con `relURL`, no `/…` a mano) |
| **Contenido de P1.2 online** | 0.5p | En la URL pública: parcial visible, segunda página, blog con ≥ 1 entrada y enlace a GitHub (P1.1) que funciona; portada sin texto de prueba |

### Más allá de lo técnico — 3 puntos

| **Criterio** | **Peso** | **Qué se valora** |
|:---|:---:|:---|
| **Cambios del día de la realización de la Prácticax2** | 1p | Las mejoras propuestas se implementan, se reconstruyen (`hugo`), se suben y se ven en la URL pública |
| **Identidad visual y calidad del contenido** | 1p | Cuidado visual ("ponlo bonico") y texto propio y específico, no placeholder |
| **Entregable completo y verificable** | 1p | URL pública + URL del repo + captura de Settings → Pages; todo comprobable |

## Convención en vivo vs. online, con matiz de `git log`

Esta práctica se entrega vía repositorio GitHub, así que se añade una comprobación objetiva (misma convención que P1.2):

- **10/10** — solo si hay demo en vivo **y** el `git log` muestra trabajo real incremental: varios commits, con marcas de tiempo realmente separadas (no todos en el mismo minuto) y mensajes no genéricos.
  Se comprueba con `git log --format='%h %ad %s' --date=iso` o `https://api.github.com/repos/<owner>/<repo>/commits`.
- **Intermedio (hasta 9/10)** — sin demo en vivo, pero con `git log` que sí muestra esa evidencia (trabajo desde terminal, "a lo Pro").
- **Tope 8/10** — sin demo en vivo y sin evidencia en `git log` (un único commit, mensajes genéricos o timestamps idénticos; típico de arrastrar ficheros desde la web de GitHub).

## Escala orientativa

- **Excelente (9-10):** sitio Hugo publicado y accesible, configuración correcta, cambios de la Prácticax2 hechos, cuidado visual, demo en vivo y/o `git log` con evidencia real.
- **Notable (7-8.9):** todo funciona, con algún detalle menor (un enlace o estilo roto, contenido escueto, o topado por ser solo-online sin `git log`).
- **Suficiente (5-6.9):** el repo está subido pero la web publicada tiene fallos importantes (sin estilos, falta blog o parcial, `docs/` desactualizado).
- **Insuficiente (<5):** no hay URL pública funcional (404, Pages mal configurado, `docs/` ausente) o el sitio no es el de Hugo.

## Lista de comprobación rápida (para nosotros, el profesorado :-)

```bash
git clone https://github.com/<alumno>/<repo>.git && cd <repo>
grep -E 'baseURL|publishDir|title' hugo.toml
ls -a docs | head                    # index.html, .nojekyll, blog/…
ls layouts/partials                  # parcial real
git log --format='%h %ad %s' --date=iso | head -20
curl -sI https://<alumno>.github.io/<repo>/ | head -1   # HTTP/2 200
```

Errores frecuentes: Pages en `/ (root)`, `baseURL` sin la subruta del repo, `draft: true`, olvidar `hugo` antes del `push`, texto de prueba en la portada.

## Plantilla de feedback (para el estudiante)

Más allá de una calificación numérica, ¿que puedes esperar por nuestra parte a modo de realimentación/crítica-constructiva? Pues algo así...

```
## Feedback
- Qué ha ido bien: …
- A mejorar: …
- ¿Has pensado en usar `git` desde la terminal para hacer los cambios de la práctica... a lo Pro? ;-)
```

"Recuerda ... KISS!" :-)
