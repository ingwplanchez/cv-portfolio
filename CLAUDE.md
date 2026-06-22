# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Portafolio web personal estático de una sola página (CV/landing page) de **Wilmer Planchez** (Ing. Mecatrónico / Python Developer). Construido con HTML + Bootstrap 5 (cargado vía CDN desde jsDelivr) + CSS personalizado mínimo. Sin JavaScript propio, sin build step, sin backend, sin base de datos.

## Comandos habituales

No hay sistema de build, linter ni tests. Para trabajar localmente basta con abrir el sitio en un navegador:

```bash
# Abrir directamente (sin servidor)
start index.html          # Windows
open index.html           # macOS
xdg-open index.html       # Linux

# O servir localmente (opcional, recomendado para verificar responsive)
python -m http.server 8000
# luego visitar http://localhost:8000
```

Para validar HTML, usar el validador del W3C: <https://validator.w3.org/>.

## Arquitectura

El proyecto es deliberadamente simple: un único documento HTML monolítico con todo el contenido hardcodeado. No hay frameworks de componentes, ni módulos JS, ni tooling.

```
index.html          ← Página completa (HTML + clases Bootstrap en línea)
css/style.css       ← Solo estilos personalizados del proyecto
img/                ← Recursos gráficos (foto perfil, cursos, proyectos, etc.)
README.md           ← Descripción del repo
info.txt            ← Notas/texto auxiliar del autor (no es código)
```

**Flujo del HTML (orden de las secciones, definido por su `id`):**

1. `header` — barra superior con redes sociales
2. `principal` — hero con foto, nombre, descripción y CTAs
3. `about` — grid de 4 habilidades (IA, Software, Web, Electrónica)
4. `courses` — cards de cursos de Udemy
5. `ia` — proyectos de IA, con subsección `agentes`
6. `web` — proyectos de desarrollo web
7. `electronica` — proyectos de electrónica, con subsección `mecatronica`
8. `contact` — footer con datos de contacto

## Convenciones de naming

- **Secciones HTML:** `<section id="kebab-case-en-espanol">`. Usar la palabra en español (`cursos`, `electronica`, `mecatronica`), no traducir al inglés.
- **Imágenes:** `kebab-case` en minúsculas (ej: `kicad-biosense-nano.jpg`, `flasktasker.png`). Excepción: las imágenes nuevas añadidas en 2025 usan prefijos en MAYÚSCULAS por categoría (`GEM-*.png` para proyectos IA tipo GEM, `IA-*.jpg` para automatizaciones con IA, `robotic-*.png` para robótica). Mantener consistencia con el prefijo de la categoría correspondiente al añadir nuevas.
- **Recursos:** siempre rutas relativas con `./` desde la raíz (`./img/foto.jpg`, `./css/style.css`).
- **CSS personalizado:** clases `kebab-case` (`.gradient-background`, `.icon-square`, `.profile-img`).
- **Idioma del contenido:** español en todo el copy visible al usuario.

## Cómo añadir contenido nuevo

El proyecto no tiene modularización: para añadir una nueva sección (por ejemplo "Proyectos destacados") o un nuevo proyecto a una sección existente, se edita directamente `index.html` insertando un `<section id="...">` en el lugar adecuado del flujo. No se crean archivos parciales ni componentes.

Si se añaden imágenes nuevas, van a `img/`. Si se necesitan estilos únicos, se añaden al final de `css/style.css` sin tocar los existentes. Los SVGs de iconos (Bootstrap Icons inline, no son archivo) se copian dentro del HTML.

## Stack y dependencias

- **Bootstrap 5.3.6** vía CDN (`https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css`) con SRI hash en el `<link>` — si se actualiza la versión, regenerar el hash de integridad en el `index.html`.
- **Bootstrap Icons** vía clases `bi bi-*` inline en el HTML (no requiere import adicional si las clases se usan como tales, pero los SVGs actuales están copiados directamente; en caso de duda revisar si el ícono se renderiza o no).
- **Sin JavaScript propio**, sin jQuery, sin dependencias npm.

## Notas operativas

- El archivo `info.txt` (~28 KB) parece ser un dump de texto auxiliar; **no modificarlo a menos que el usuario lo pida explícitamente**, podría ser contenido generado o de referencia personal.
- El repositorio usa español en todo el contenido visible; mantener ese idioma al añadir copy nuevo.
- El owner es **Wilmer Planchez** (git config: `Wilmer Planchez`). No hacer commits ni push sin instrucción explícita.
