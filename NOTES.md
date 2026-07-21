# Notas técnicas — TecnoCompara

## 1. Contexto

- Sitio de comparativas de electrónica en Perú (celulares, TVs, refrigeradoras).
- Samsung es el advertiser objetivo en Awin, no un riesgo a evitar — las 3
  categorías elegidas coinciden con donde Samsung tiene presencia fuerte
  (Galaxy, QLED/Neo QLED, Family Hub).
- Dominio: **tech.modoahorro.pe** (subdominio, repo separado de ModoAhorro).
- Buena práctica FTC/Awin: declarar en "Sobre mí" que el sitio tiene enlaces
  de afiliado con comisión (ya está escrito en `sobre-mi.md`). No es
  necesario revelar el empleador.

## 2. Pasos para subir el repo y activar GitHub Pages

1. Crear el repositorio **`tecnocompara`** en GitHub (separado del de
   ModoAhorro).
2. Subir este proyecto:
   ```bash
   cd tecnocompara
   git init
   git add .
   git commit -m "Setup inicial del sitio TecnoCompara"
   git branch -M main
   git remote add origin https://github.com/<tu-usuario>/tecnocompara.git
   git push -u origin main
   ```
3. En GitHub → **Settings → Pages**:
   - Source: `Deploy from a branch`
   - Branch: `main` / `/ (root)`
   - Custom domain: `tech.modoahorro.pe` (GitHub genera su propio `CNAME`
     en este repo — es independiente del `CNAME` de `modoahorro.pe`, que
     vive en su propio repo).

## 3. DNS en NIC.pe

En el mismo panel donde ya está configurado `modoahorro.pe`, agregar un
registro **nuevo** (no reemplaza nada existente):

```
Nombre: tech
Tipo:   CNAME
Valor:  cguillenh22.github.io
```

Esperar "DNS check successful" en GitHub Pages y luego activar
**"Enforce HTTPS"** — mismo proceso que en ModoAhorro.

## 4. GTM y GA4 — cuentas NUEVAS

- No reutilizar el contenedor GTM ni la propiedad GA4 de ModoAhorro.
- Crear:
  - Un contenedor **GTM nuevo** para `tech.modoahorro.pe`.
  - Una propiedad **GA4 nueva** para este sitio.
- Reemplazar en `_config.yml`:
  ```yaml
  gtm_container_id: "GTM-XXXXXXX"   # ID real del contenedor nuevo
  ga4_measurement_id: "G-XXXXXXXXXX" # ID real de la propiedad nueva
  ```
  El snippet de GTM (`_includes/gtm-head.html` y `gtm-body.html`) solo se
  inyecta automáticamente cuando el ID deja de ser el placeholder.

## 5. Awin — activar/buscar el advertiser de Samsung

1. Entrar a la cuenta de Awin → **Find Advertisers**.
2. Cambiar el filtro de **Sector** de "Finance & Insurance" a
   "Retail & Shopping" (o buscar subcategoría "Electronics" si existe).
3. Buscar directamente **"Samsung"** en la barra de búsqueda del directorio.
4. Verificar que **Region → Peru** siga marcado.
5. Si aparece "Samsung PE" o similar con **Link Status verde**, revisar antes
   de aplicar:
   - Comisión
   - Cookie window
   - Feed de productos
6. Si no aparece nada específico para Perú, revisar si existe un programa
   regional **LATAM** que acepte tráfico peruano.

## 6. Tracking de clics de afiliado (GTM)

En el contenedor GTM **nuevo** de este sitio:

1. **Trigger personalizado:** "Click - Just Links", con condición de que la
   URL de destino contenga el dominio de tracking de Awin (normalmente
   `awin1.com` o `zenaps.com` — confirmar el dominio exacto una vez que Awin
   genere los deep links reales).
2. **Tag:** GA4 Event → nombre del evento `click_afiliado`.
3. **Parámetros del evento:**
   - `advertiser` (ej. `"Samsung"`)
   - `producto` (artículo/página donde ocurrió el clic)
   - `posicion` (cuerpo del artículo, botón CTA, etc.)
4. Publicar el tag y verificar en **modo Preview** de GTM que se dispara al
   hacer clic en un link de prueba.

Esto permite filtrar en GA4 qué artículos generan más clics hacia Samsung —
la métrica clave para justificar el canal ante el lead/cliente.

## 7. Identidad visual (ya implementada en `assets/css/main.css`)

- **Paleta:** grafito/carbón (`#1A1D21`) como base + coral/naranja
  (`#FF5A2E`) como acento. Deliberadamente **sin azul** — evita parecer un
  sitio "casi oficial" de Samsung y diferencia de todas las marcas grandes
  de electrónica, no solo de Samsung.
- **Tipografía:** Space Grotesk (títulos, geométrica/moderna) + Inter
  (cuerpo) + JetBrains Mono (specs, metadatos, breadcrumbs) — se lee
  "tech/preciso" en vez de "editorial/cálido" (a diferencia de
  ModoAhorro/Camino21, que usan serif editorial).
- **Elemento distintivo:** `.spec-strip` — ficha de datos en mono, pensada
  para mostrar specs comparables de un vistazo dentro del artículo.

## 8. Estructura de contenido — evergreen vs. volátil

- Cada artículo declara `content_type: "evergreen"` o `"volatil"` en el
  front matter.
- **Evergreen:** no caduca (ej. "cómo elegir un celular según tu uso").
- **Volátil:** requiere revisión real de contenido cada 2-3 meses, no solo
  actualizar `date_modified` (ej. "mejores celulares Perú [mes-año]").
- Mezcla recomendada para los primeros 50 artículos: **60% evergreen / 40%
  volátil**.
- Pendiente futuro: script/reporte que liste artículos `volatil` con más de
  90 días sin revisión (no implementado todavía).

## 9. Checklist de validación antes de publicar

- [ ] `_layouts/default.html` y `_layouts/articulo.html` existen en el repo
      (si falta uno, Jekyll solo da *warning*, no error — el build queda
      verde pero el artículo se ve sin header/nav/footer; esto ya pasó una
      vez en ModoAhorro).
- [ ] El artículo tiene `categories` válidas según `_data/categories.yml`.
- [ ] IDs de GTM/GA4 reemplazados con las cuentas **nuevas** de este sitio.
- [ ] Enlaces de afiliado con `rel="sponsored nofollow noopener"`.
- [ ] Sitemap (`jekyll-sitemap`) generándose en `/sitemap.xml` tras el build.
- [ ] Trigger de GTM probado en modo Preview antes de publicar en producción.

## 10. Pendientes (fuera de este setup inicial)

- Newsletter (Mailchimp) — no configurado, esperando decisión de herramienta.
- Formulario de contacto/dudas (Formspree) — no configurado.
- Consent mode de cookies — solo necesario si se activa Google Ads o hay
  tráfico relevante de la UE.
- Investigación de keywords: además de Keyword Planner, revisar **Google
  Trends** por estacionalidad (Cyber Days, Navidad, Fiestas Patrias) — la
  demanda de electrónica varía fuerte por fecha, a diferencia de finanzas.
  Programar contenido volátil **antes** de esos picos, no durante.
