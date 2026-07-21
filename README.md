# TecnoCompara

Sitio de comparativas de electrónica (celulares, TVs, refrigeradoras) para
el mercado peruano. Jekyll + GitHub Pages, alojado en el subdominio
`tech.modoahorro.pe`.

## Desarrollo local

```bash
bundle install
bundle exec jekyll serve
```

Sitio disponible en `http://localhost:4000`.

## Estructura

- `_articulos/` — artículos (colección `articulos`), un archivo `.md` por pieza.
- `_layouts/default.html` — layout base (home, categorías, sobre-mí).
- `_layouts/articulo.html` — layout de artículo (breadcrumbs, specs, FAQ, relacionados).
- `_data/categories.yml` — nombres visibles de cada categoría.
- `assets/css/main.css` — sistema de diseño (grafito + coral).
- `sobre-mi.md` — declaración de afiliados (obligatoria por Awin/FTC).

## Front matter de un artículo

```yaml
---
title: "Título del artículo"
seo_title: "Título SEO opcional | TecnoCompara"
description: "Meta description"
categories: [celulares, guias-compra]   # la primera define breadcrumb y agrupación
content_type: "evergreen"                # o "volatil"
read_time: 7
date: 2026-07-20
date_modified: 2026-07-20
faq:                                      # opcional, genera schema FAQPage
  - q: "Pregunta"
    a: "Respuesta"
---
```

## Antes de publicar (checklist)

1. `_layouts/articulo.html` y `_layouts/default.html` existen en el repo
   (Jekyll solo da *warning*, no error, si falta un layout — el build queda
   verde pero el artículo se ve sin header/footer).
2. El artículo tiene al menos una categoría válida de `_data/categories.yml`.
3. Los IDs de GTM (`gtm_container_id`) y GA4 en `_config.yml` están
   reemplazados (cuenta **nueva**, no la de ModoAhorro).
3. Los enlaces de afiliado llevan `rel="sponsored nofollow noopener"`.
4. Revisar `NOTES.md` para los pasos de DNS, Awin y tracking de clics.

Ver `NOTES.md` para el detalle de configuración técnica (DNS, GTM/GA4, Awin,
tracking de clics de afiliado).
