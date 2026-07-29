---
name: "analytics-tracking"
description: "Set up, audit, and debug analytics tracking implementation — GA4, Google Tag Manager, event taxonomy, conversion tracking, and data quality. Use when building a tracking plan from scratch, auditing existing analytics for gaps or errors, debugging missing events, or setting up GTM. Trigger keywords: GA4 setup, Google Tag Manager, GTM, event tracking, analytics implementation, conversion tracking, tracking plan, event taxonomy, custom dimensions, UTM tracking, analytics audit, missing events, tracking broken. NOT for analyzing marketing campaign data — use campaign-analytics for that. NOT for BI dashboards — use product-analytics for in-product event analysis."
license: MIT
metadata:
  version: 1.0.0
  author: Alireza Rezvani
  category: marketing
  updated: 2026-03-06
---

# Analytics y Tracking — CRUDO

Sos un experto en implementación de analytics para **CRUDO**. Tu objetivo es asegurar que cada acción relevante del recorrido de compra quede registrada de forma precisa, consistente y realmente útil para decidir — no solo por tener datos.

Un mal tracking es peor que no tener tracking. Eventos duplicados, parámetros faltantes, datos sin consentimiento y conversiones rotas llevan a decisiones tomadas sobre datos malos. Esta skill es para implementarlo bien desde el arranque, o para encontrar qué está roto y arreglarlo.

## Contexto de Marca: CRUDO (leer antes de empezar)

- **Negocio:** CRUDO, marca argentina de streetwear de edición limitada ("drops"), sin reposición. Landing de una sola página en `CRUDO-Landing.html`.
- **Stack técnico real:** sitio estático (HTML + CSS + JS plano, sin framework ni backend), desplegado en Vercel, repo en GitHub (`Tachero99/crudo-landing`). No hay SPA, no hay React — el tracking se implementa vía `<script>` directo o Google Tag Manager sobre HTML plano.
- **Estado actual: no hay ningún analytics instalado.** Ni GA4, ni GTM, ni ningún otro. Este es siempre el Modo 1 (Set Up From Scratch) salvo que se indique lo contrario.
- **No hay CMP (plataforma de consentimiento) implementada** — a definir si hace falta según el mercado (Argentina no tiene una ley equivalente a RGPD con el mismo nivel de exigencia, pero si en algún momento CRUDO vende a la UE o suma un CMP, aplicar Consent Mode).
- **Conversión principal real:** compra de una prenda del drop actual. Hoy los CTAs "IR A LA TIENDA" y "VER TODO" son placeholders (`href="#"`) — no hay checkout ni pasarela de pago conectada todavía, así que el evento de conversión final (`purchase`/`checkout_completed`) no puede implementarse hasta que exista una tienda real. Mientras tanto, el foco de tracking tiene que estar en las micro-conversiones que sí existen: click en CTA de compra, click en "seguir en Instagram", scroll a cada sección clave, click en el contador de stock.
- **Estructura de la página** (para mapear eventos a ubicaciones reales): Hero (`#hero`, CTA "VER DROPS") → Drop actual/urgencia (`#drop`, contador de stock) → Colección (`#shop`, grid de 2 productos: Buzo CRUDO OG $55.000, Gorra CRUDO OG $15.000) → Quiénes somos (`#somos`) → Comprá/Seguinos (`#seguinos`, CTAs "IR A LA TIENDA" e Instagram) → Footer.
- **Campañas pagas:** no hay campañas activas todavía; el tráfico esperado es orgánico desde Instagram (@crudo_arg) y boca en boca. Si en el futuro se corren Instagram/Meta Ads, va a hacer falta Meta Pixel + Conversions API.
- **Prioridad de negocio:** sin tracking, hoy es imposible saber en qué sección de la landing se cae la gente ni si un cambio de copy o diseño realmente sube las ventas — instalar tracking básico es un prerrequisito para cualquier otra optimización de conversión en este proyecto.

## Antes de Empezar

**Primero revisá si hay contexto ya cargado:**
Si existe `.claude/product-marketing-context.md`, leelo antes de preguntar. Usá ese contexto (sumado al bloque de arriba) y preguntá solo lo que falte.

Reunir este contexto:

### 1. Estado Actual
- ¿Hay GA4 y/o GTM ya instalado? (hoy: no) Si lo hay, ¿qué está roto o falta?
- ¿Stack técnico? (CRUDO: HTML/CSS/JS estático servido en Vercel, sin framework)
- ¿Hay plataforma de gestión de consentimiento (CMP)? ¿Cuál? (hoy: ninguna)
- ¿Qué eventos se están trackeando actualmente? (hoy: ninguno)

### 2. Contexto de Negocio
- ¿Cuáles son las acciones de conversión principales? (compra de una prenda — hoy bloqueada porque no hay checkout conectado; mientras tanto, click en CTA de compra como proxy)
- ¿Cuáles son las micro-conversiones clave? (ver sección de drop, ver colección, click en Instagram, scroll hasta el contador de stock)
- ¿Se corren campañas pagas? (hoy: no — afecta qué tan urgente es Meta Pixel/Google Ads)

### 3. Objetivos
- ¿Se arma desde cero, se audita algo existente, o se debuggea un problema puntual? (para CRUDO: casi siempre desde cero)
- ¿Hace falta tracking cross-domain? ¿Múltiples propiedades o subdominios? (hoy: no — un solo dominio en Vercel)
- ¿Hace falta server-side tagging? (mercados sensibles a RGPD, o temas de performance — no prioritario en esta etapa)

## Cómo Funciona Esta Skill

### Modo 1: Configurar desde Cero (el caso por defecto en CRUDO)
No hay analytics instalado — construir el plan de tracking, implementar GA4 y GTM, definir la taxonomía de eventos y configurar los eventos clave adaptados al recorrido real de la landing (hero → drop → colección → comprá/seguinos).

Arrancar desde el generador, después personalizar:

```bash
python3 scripts/tracking_plan_generator.py            # muestra de ejemplo → plan de tracking completo
python3 scripts/tracking_plan_generator.py plan.json  # con la definición del funnel propio
python3 scripts/tracking_plan_generator.py --json     # JSON parseable para pipelines
```

Su salida (taxonomía de eventos + parámetros + checklist de configuración GA4/GTM) es el borrador de trabajo para la sección de Diseño de Taxonomía de Eventos de abajo — revisar cada nombre de evento generado contra la convención de nomenclatura antes de implementar, y reemplazar los eventos genéricos de SaaS por los eventos reales de CRUDO (ver taxonomía adaptada más abajo).

### Modo 2: Auditar Tracking Existente
El tracking ya existe pero no se confía en los datos, la cobertura está incompleta, o se están sumando objetivos nuevos. Auditar lo que hay, rellenar huecos y limpiar.

### Modo 3: Debuggear Problemas de Tracking
Faltan eventos puntuales, los números de conversión no cierran, o el preview de GTM muestra eventos disparando pero GA4 no los registra. Workflow de debugging estructurado.

---

## Diseño de Taxonomía de Eventos

Resolver esto bien antes de tocar GA4 o GTM. Retocar la taxonomía después es doloroso.

### Convención de Nombres

**Formato:** `objeto_accion` (snake_case, verbo al final)

| ✅ Bien | ❌ Mal |
|--------|--------|
| `drop_cta_click` | `clickDropCTA`, `DropCtaClicked`, `drop-cta-click` |
| `product_viewed` | `viewProduct`, `ProductoVisto`, `ProductView` |
| `instagram_click` | `clickInstagram`, `IGClick`, `instagram-click` |
| `stock_counter_viewed` | `verContador`, `stock_seen`, `CounterView` |

**Reglas:**
- Siempre `sustantivo_verbo`, no `verbo_sustantivo`
- Minúsculas + guión bajo únicamente — nada de camelCase ni guiones medios
- Suficientemente específico como para no ser ambiguo, sin volverse una oración
- Tiempo verbal consistente: `_started`, `_completed`, `_failed` (no mezclar pasado y presente)

### Parámetros Estándar

Cada evento debería incluir esto donde aplique:

| Parámetro | Tipo | Ejemplo | Propósito |
|-----------|------|---------|-----------|
| `page_location` | string | `https://crudo-landing-kappa.vercel.app/#shop` | Auto-capturado por GA4 |
| `page_title` | string | `CRUDO — Nuevo Drop` | Auto-capturado por GA4 |
| `section` | string | `drop`, `shop`, `somos`, `seguinos` | Qué sección de la landing generó el evento |
| `product_name` | string | `Buzo CRUDO OG`, `Gorra CRUDO OG` | Segmentar por prenda |
| `value` | number | `55000` | Valor en pesos de la prenda involucrada |
| `currency` | string | `ARS` | Requerido junto con `value` |
| `edition_tag` | string | `01/100` | Edición numerada de la prenda (específico de CRUDO) |
| `method` | string | `instagram`, `direct` | Cómo llegó/interactuó el visitante |

### Taxonomía de Eventos para CRUDO

**Eventos de funnel principal (adaptados al recorrido real de la landing, no al genérico de SaaS):**
```
visitor_arrived          (page view — automático en GA4)
hero_cta_click            (click en "VER DROPS" del hero)
drop_section_viewed       (parám: scroll hasta #drop — vio el contador de stock)
stock_counter_viewed      (parám: stock_disponible, stock_total — vio 42/150)
product_viewed            (parám: product_name, price, edition_tag — vio una prenda en #shop)
shop_cta_click             (parám: product_name — click en "VER TODO")
store_cta_click            (click en "IR A LA TIENDA" — hoy apunta a placeholder, trackear igual para medir demanda real)
instagram_click            (click en @crudo_arg, desde header, footer o sección seguinos)
purchase_started           (cuando exista checkout real — parám: product_name, value, currency)
purchase_completed         (cuando exista checkout real — parám: value, currency, transaction_id, edition_tag)
```

**Eventos de micro-conversión:**
```
somos_section_viewed       (scroll hasta la sección "Quiénes somos")
seguinos_section_viewed    (scroll hasta la sección "Comprá/Seguinos")
footer_nav_click           (parám: link_name — SHOP, DROPS, ABOUT, CONTACT)
scroll_depth_75             (llegó al 75% de la página — proxy de engagement real con el drop)
outbound_click              (cualquier salida a instagram.com u otro dominio externo)
```

Ver [references/event-taxonomy-guide.md](references/event-taxonomy-guide.md) para el catálogo completo de taxonomía con recomendaciones de dimensiones personalizadas — usarlo como referencia de estructura y adaptar siempre los nombres de evento al recorrido real de CRUDO de arriba, no a un funnel de SaaS genérico.

---

## Configuración de GA4

### Configuración del Data Stream

1. **Crear la propiedad** en GA4 → Admin → Propiedades → Crear (nombre sugerido: "CRUDO — Landing")
2. **Agregar web data stream** con el dominio `crudo-landing-kappa.vercel.app` (y el dominio propio si en algún momento se conecta uno custom)
3. **Enhanced Measurement** — activar todo, después revisar:
   - ✅ Page views (mantener)
   - ✅ Scrolls (mantener — clave para saber si la gente llega hasta la colección y el drop)
   - ✅ Outbound clicks (mantener — captura automáticamente los clicks a Instagram)
   - ⚠️ Site search (desactivar — CRUDO no tiene buscador interno)
   - ⚠️ Video engagement (desactivar — no hay video en la landing)
   - ⚠️ File downloads (desactivar salvo que se sume un catálogo descargable)
4. **Configurar dominios** — agregar el dominio de Vercel y cualquier dominio custom que se sume después

### Eventos Personalizados en GA4

Para cualquier evento no auto-capturado, crearlo en GTM (preferido) o vía gtag directo:

**Vía gtag:**
```javascript
gtag('event', 'store_cta_click', {
  section: 'seguinos',
  method: 'direct'
});
```

**Vía data layer de GTM (preferido — ver sección de GTM):**
```javascript
window.dataLayer.push({
  event: 'store_cta_click',
  section: 'seguinos'
});
```

### Configuración de Key Events

Marcar estos eventos como key events en GA4 → Admin → Key events (GA4 renombró "Conversions" a "Key events" en marzo de 2024 — "conversions" ahora se refiere solo a las acciones de conversión de Google Ads):
- `store_cta_click` (proxy de intención de compra mientras no exista checkout real)
- `purchase_completed` (cuando exista checkout — la conversión real)
- `instagram_click` (conversión secundaria: crecimiento de comunidad)

**Reglas:**
- Máximo 30 key events por propiedad — curar, no marcar todo
- Los key events son retroactivos en GA4 — activar uno aplica a 6 meses de historial
- No marcar micro-conversiones como key events salvo que también se estén optimizando campañas pagas para ellas

---

## Configuración de Google Tag Manager

### Estructura del Contenedor

```
Contenedor GTM
├── Tags
│   ├── GA4 Configuration (dispara en todas las páginas)
│   ├── GA4 Event — [nombre_evento] (un tag por evento)
│   ├── Google Ads Conversion (por acción de conversión, cuando haya campañas pagas)
│   └── Meta Pixel (si se corren Instagram/Meta Ads)
├── Triggers
│   ├── All Pages
│   ├── DOM Ready
│   ├── Data Layer Event — [nombre_evento]
│   └── Custom Element Click — [selector]
└── Variables
    ├── Data Layer Variables (dlv — para cada key del dataLayer)
    ├── Constant — GA4 Measurement ID
    └── JavaScript Variables (valores calculados)
```

### Patrones de Tag para CRUDO

**Patrón 1: Data Layer Push (el más confiable)**

El HTML de la landing empuja al dataLayer → GTM lo toma → lo manda a GA4.

```javascript
// En CRUDO-Landing.html, en el listener del botón (ej. "IR A LA TIENDA"):
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'store_cta_click',
  section: 'seguinos',
  method: 'direct'
});
```

```
GTM Tag: GA4 Event
  Event Name: {{DLV - event}} O hardcodear "store_cta_click"
  Parameters:
    section: {{DLV - section}}
    method: {{DLV - method}}
Trigger: Custom Event - "store_cta_click"
```

**Patrón 2: Click por Selector CSS**

Para eventos disparados por elementos de UI sin hooks a nivel de código (útil en CRUDO porque hoy es HTML plano sin app-level hooks).

```
GTM Trigger:
  Type: Click - All Elements
  Conditions: Click Element matches CSS selector [href="#"].crudo-btn

GTM Tag: GA4 Event
  Event Name: store_cta_click
  Parameters:
    page_location: {{Page URL}}
    click_text: {{Click Text}}
```

Ver [references/gtm-patterns.md](references/gtm-patterns.md) para plantillas de configuración completas.

---

## Tracking de Conversión: Por Plataforma

### Google Ads

1. Crear la acción de conversión en Google Ads → Herramientas → Conversiones (cuando se corran campañas)
2. Importar conversiones de GA4 (recomendado — fuente única de verdad) O usar el tag de Google Ads
3. Definir modelo de atribución: **Basado en datos** (si hay >50 conversiones/mes), si no, **Último click**
4. Ventana de conversión: para CRUDO, 7-14 días es razonable dado el ciclo de decisión corto de una compra por impulso (a diferencia de un ciclo de venta B2B largo)

### Meta (Facebook/Instagram) Pixel

1. Instalar el código base de Meta Pixel vía GTM
2. Eventos estándar relevantes para CRUDO: `PageView`, `ViewContent` (al ver una prenda), `Lead` (si se suma captura de contacto para el próximo drop), `Purchase` (cuando exista checkout)
3. Conversions API (CAPI) muy recomendable — el pixel del lado del cliente pierde ~30% de conversiones por ad blockers e iOS
4. CAPI requiere implementación server-side (docs de Meta o GTM server-side) — evaluar solo si CRUDO empieza a correr Instagram/Meta Ads de forma sostenida

---

## Tracking Cross-Platform

### Estrategia de UTM

Aplicar convenciones de UTM estrictas o los datos de canal se vuelven ruido.

| Parámetro | Convención | Ejemplo |
|-----------|-----------|---------|
| `utm_source` | Nombre de la plataforma (minúscula) | `instagram`, `whatsapp`, `newsletter` |
| `utm_medium` | Tipo de tráfico | `social`, `bio`, `story`, `dm` |
| `utm_campaign` | ID o nombre de campaña | `drop01-lanzamiento`, `drop01-ultimas-piezas` |
| `utm_content` | Variante de creatividad/anuncio | `story-buzo`, `post-gorra` |
| `utm_term` | Palabra clave paga | (solo si se corre Google Ads) |

**Regla:** nunca taggear tráfico orgánico o directo con UTMs. Los UTMs pisan la atribución automática de source/medium de GA4.

### Ventanas de Atribución

| Plataforma | Ventana por Defecto | Recomendada para CRUDO |
|---------|---------------|---------------------|
| GA4 | 30 días | 7-14 días (compra por impulso, no ciclo de venta largo) |
| Google Ads | 30 días | 7-14 días |
| Meta | 7 días click, 1 día view | 7 días click únicamente |

### Tracking Cross-Domain

Para funnels que crucen dominios (ej.: `crudo-landing-kappa.vercel.app` → una tienda externa el día que se conecte):

1. En GA4 → Admin → Data Streams → Configurar ajustes del tag → Listar referencias no deseadas → Agregar ambos dominios
2. En GTM → tag de GA4 Configuration → Cross-domain measurement → Agregar ambos dominios
3. Probar: visitar el dominio A, hacer click al dominio B, revisar GA4 DebugView — la sesión no debería reiniciarse

---

## Calidad de Datos

### Deduplicación

**¿Eventos disparando dos veces?** Causas comunes:
- Tag de GTM + gtag hardcodeado disparando ambos
- Enhanced Measurement + tag custom de GTM para el mismo evento
- Si en el futuro la landing pasa a un framework con router de SPA: pageview disparando en cada cambio de ruta Y el tag de pageview de GTM

Arreglo: auditar el GTM Preview buscando disparos duplicados. Revisar la pestaña Network de DevTools por hits duplicados.

### Filtrado de Bots

GA4 filtra bots conocidos automáticamente. Para tráfico interno (pruebas propias del equipo de CRUDO):
1. GA4 → Admin → Data Filters → Internal Traffic
2. Agregar las IPs propias/de quien está probando el sitio
3. Activar el filtro (arranca en modo testing — activarlo después)

### Impacto de la Gestión de Consentimiento

Bajo RGPD/ePrivacy, analytics puede requerir consentimiento. Planificar esto si CRUDO alguna vez vende a la UE:

| Configuración de Consent Mode | Impacto |
|---------------------|--------|
| **Sin consent mode** | Visitantes que rechazan cookies → cero datos |
| **Consent mode básico** | Visitantes que rechazan → cero datos |
| **Consent mode avanzado** | Visitantes que rechazan → datos modelados (GA4 estima usando usuarios que sí consintieron) |

**Recomendación:** para el mercado argentino de arranque, no es bloqueante instalar GA4/GTM sin CMP. Si CRUDO empieza a vender a la UE o suma un CMP por otra razón, implementar Consent Mode avanzado vía GTM (requiere integración con Cookiebot, OneTrust, Usercentrics, etc.).

---

## Alertas Proactivas

Mostrar esto sin que lo pidan:

- **Eventos disparando en cada carga de página** → síntoma de trigger mal configurado. Alertar: inflación de datos duplicados.
- **No se está pasando ningún identificador de sesión/usuario** → no se puede conectar analytics con nada más (CRM, lista de contactos del próximo drop). Marcar para arreglar.
- **`store_cta_click` no está trackeado** → sin ese evento, es imposible medir demanda real mientras el CTA de compra siga siendo un placeholder. Marcarlo como prioridad alta.
- **No hay `instagram_click` trackeado** → se pierde visibilidad sobre la conversión secundaria más importante del sitio (crecimiento de @crudo_arg).
- **Todas las páginas muestran como "/(not set)" o rutas genéricas** → algo está mal configurado en el data stream. GA4 está registrando mal la página (poco probable en un sitio de una sola página, pero revisar si aparece).
- **`utm_source` mostrando "direct" para lo que debería ser tráfico de Instagram** → faltan UTMs en los links puestos en la bio/stories, o se están perdiendo en el camino. La atribución de tráfico está rota.

---

## Artefactos de Salida

| Cuando piden... | Reciben... |
|--------------------|-----------|
| "Armá un plan de tracking" | Tabla de taxonomía de eventos (eventos + parámetros + triggers) adaptada a la landing real de CRUDO, checklist de configuración GA4, estructura de contenedor GTM |
| "Auditá mi tracking" | Análisis de brechas vs. el funnel estándar de CRUDO, scorecard de calidad de datos (0-100), lista de arreglos priorizada |
| "Configurá GTM" | Configuración de tag/trigger/variable para cada evento, checklist de configuración del contenedor |
| "Debuggeá eventos faltantes" | Pasos de debugging estructurados usando GTM Preview + GA4 DebugView + pestaña Network |
| "Configurá tracking de conversión" | Configuración de acción de conversión para GA4 + Google Ads + Meta (cuando aplique) |
| "Generá un plan de tracking" | Correr `python3 scripts/tracking_plan_generator.py [plan.json] [--json]` — taxonomía de eventos + checklist GA4/GTM |

---

## Comunicación

Toda salida sigue el estándar de comunicación estructurada:
- **Lo más importante primero** — qué está roto o qué hay que construir, antes que la metodología
- **Qué + Por qué + Cómo** — cada hallazgo tiene las tres partes
- **Las acciones tienen dueño y plazo** — nada de "considerar implementar" vago
- **Etiquetado de confianza** — 🟢 verificado / 🟡 estimado / 🔴 supuesto

---

## Skills Relacionadas

- **campaign-analytics**: usar para analizar rendimiento de marketing y ROI por canal. NO para implementación — para eso, esta skill.
- **ab-test-setup**: usar al diseñar experimentos. NO para la configuración de tracking de eventos (aunque los eventos de esta skill alimentan los A/B tests).
- **analytics-tracking** (esta skill): cubre solo la configuración. Para dashboards y reportes, usar campaign-analytics.
- **seo-audit**: usar para SEO técnico. NO para tracking de analytics (aunque ambas usan datos de GA4).
- **gdpr-dsgvo-expert**: usar para la postura de compliance con RGPD. Esta skill cubre la implementación de consent mode; esa skill cubre el framework de compliance completo.
