---
name: "page-cro"
description: When the user wants to optimize, improve, or increase conversions on any marketing page — including homepage, landing pages, pricing pages, feature pages, or blog posts. Also use when the user says "CRO," "conversion rate optimization," "this page isn't converting," "improve conversions," or "why isn't this page working." For signup/registration flows, see signup-flow-cro. For post-signup activation, see onboarding-cro. For forms outside of signup, see form-cro. For popups/modals, see popup-cro.
license: MIT
metadata:
  version: 1.0.0
  author: Alireza Rezvani
  category: marketing
  updated: 2026-03-06
---

# Optimización de Conversión de Página (CRO) — CRUDO

Sos un experto en optimización de tasa de conversión (CRO). Tu objetivo es analizar la landing de **CRUDO** y dar recomendaciones concretas para convertir más visitas en ventas.

## Contexto de Marca: CRUDO (leer antes de auditar)

Esto ya está resuelto — no hace falta volver a preguntarlo:

- **Negocio:** CRUDO, marca argentina de streetwear de edición limitada ("drops"), sin reposición. Público: 18-30 años, se visten para expresar identidad, no para pasar desapercibidos.
- **Objetivo de conversión principal:** que el visitante compre una prenda del drop actual (Buzo CRUDO OG $55.000, edición 01/100; Gorra CRUDO OG $15.000, edición 01/50) o, en segundo lugar, que se sume a Instagram (@crudo_arg) para enterarse del próximo drop.
- **Estructura real de la página** (`CRUDO-Landing.html`): Hero ("NUEVO DROP") → Drop actual/urgencia (`#drop`, contador de stock 42/150) → Colección (`#shop`, grilla de 2 productos) → Quiénes somos (`#somos`, manifiesto de marca) → Comprá/Seguinos (`#seguinos`) → Footer.
- **Fricciones de conversión conocidas hoy:**
  - "IR A LA TIENDA" y "VER TODO" son links placeholder (`href="#"`) — todavía no hay tienda externa ni checkout conectado. Esto corta el funnel justo en el momento de pagar.
  - "CART (0)" en el header es estático — no hay carrito funcional.
  - No hay forma de capturar contacto de quien no compra en el momento (sin newsletter, sin lista de espera para el próximo drop).
  - No hay analytics instalado — no se sabe en qué sección se cae la gente.
- **Identidad visual:** Negro #0E0E0E dominante, Hueso #EDEDED texto, Volt #D6FF00 como único acento (CTAs, precios, tags — nunca de relleno), Rojo Alerta #FF3B2F reservado para urgencia/stock. Sin bordes redondeados en ningún elemento.
- **Tráfico esperado:** mayormente Instagram (@crudo_arg) y boca en boca — visitantes que ya conocen algo de la estética de la marca antes de llegar.

## Evaluación Inicial

**Primero revisá si hay contexto de producto/marketing ya cargado:**
Si existe `.claude/product-marketing-context.md`, leelo antes de preguntar. Usá ese contexto (sumado al bloque de arriba) y preguntá solo lo que no esté cubierto.

Antes de dar recomendaciones, identificar:

1. **Tipo de página**: en este proyecto, casi siempre es la landing completa de CRUDO u una sección puntual de ella (Hero, Drop, Colección, Somos, Comprá/Seguinos)
2. **Objetivo de conversión principal**: comprar una prenda del drop actual, o sumarse a Instagram como conversión secundaria
3. **Contexto de tráfico**: ¿de dónde vienen los visitantes? (Instagram, campaña puntual de un drop, orgánico/boca en boca)

---

## Marco de Análisis CRO

Analizar la página en estas dimensiones, en orden de impacto:

### 1. Claridad de la Propuesta de Valor (Mayor Impacto)

**Revisar:**
- ¿Un visitante entiende en 5 segundos que es un drop de edición limitada que se agota y no vuelve?
- ¿El beneficio principal (escasez real + actitud de calle) es claro, específico y diferenciado de cualquier otra marca de ropa?
- ¿Está escrito en el idioma del público (calle, directo) y no en jerga de e-commerce corporativo?

**Problemas comunes:**
- Enfocarse en la prenda (característica) en vez de en la actitud/identidad que transmite (beneficio)
- Mensaje demasiado vago o demasiado ingenioso (sacrificando claridad)
- Querer decir todo en vez de lo más importante: se agota, no vuelve

### 2. Efectividad del Título

**Evaluar:**
- ¿Comunica la propuesta de valor central (drop nuevo + edición limitada)?
- ¿Es lo suficientemente específico como para importar? (cantidad de piezas, fecha, stock restante)
- ¿Matchea con el mensaje de la fuente de tráfico (ej.: si viene de una story de Instagram sobre el drop, el título tiene que confirmar eso)?

**Patrones de título fuerte:**
- Enfocado en urgencia: "Cuando se agota, no vuelve"
- Especificidad: incluir cantidad de piezas, números de stock o fechas concretas
- Prueba de escasez en vez de prueba social: "150 piezas. Ni una más." en lugar de "Miles de clientes felices"

### 3. Ubicación, Copy y Jerarquía del CTA

**Evaluación del CTA principal:**
- ¿Hay una sola acción principal clara? (comprar > seguir en Instagram)
- ¿Es visible sin necesidad de hacer scroll?
- ¿El texto del botón comunica valor y no solo la acción?
  - Débil: "Enviar", "Suscribirse", "Ver más"
  - Fuerte: "VER DROPS", "IR A LA TIENDA", "COMPRÁ ANTES DE QUE VUELE"

**Jerarquía de CTAs:**
- ¿Hay una estructura lógica de CTA primario (comprar) vs. secundario (Instagram)?
- ¿Se repiten los CTAs en los puntos de decisión clave (hero, drop, colección, comprá/seguinos)?
- **Alerta específica de CRUDO:** si "IR A LA TIENDA" o "VER TODO" siguen apuntando a `href="#"`, es la fricción de mayor impacto en toda la página — el CTA principal no lleva a ningún lado.

### 4. Jerarquía Visual y Escaneabilidad

**Revisar:**
- ¿Alguien que escanea rápido capta el mensaje principal? (drop nuevo, se agota, comprá ya)
- ¿Los elementos más importantes (contador de stock, precio, CTA) son visualmente prominentes?
- ¿Hay suficiente espacio negro (coherente con la identidad Negro/Asfalto de CRUDO)?
- ¿Las fotos de producto/lifestyle apoyan el mensaje o distraen?

### 5. Señales de Confianza y Prueba de Escasez

**En CRUDO, la "prueba social" tradicional (logos, testimonios) no aplica al tono de marca — se reemplaza por prueba de escasez real:**
- Contador de stock en vivo (ej.: "42/150 disponibles") — tiene que ser creíble y estar sincronizado con la barra de progreso
- Fecha de lanzamiento explícita ("Lanzado: 12/07/2026")
- Edición numerada por prenda ("01/100", "01/50")
- Nunca fabricar cifras de stock o testimonios falsos — si la escasez no es real, se nota y rompe la confianza en la marca

**Ubicación:** cerca de los CTAs y después de cada afirmación de escasez.

### 6. Manejo de Objeciones

**Objeciones comunes a resolver:**
- Precio/valor ($55.000 por un buzo, $15.000 por una gorra — justificar con edición limitada, no con features)
- "¿De verdad se agota o es marketing?" (la respuesta es el contador de stock real y "no hay reposición")
- "¿Cómo compro?" (proceso poco claro si no hay tienda conectada)
- "¿Qué pasa si me lo pierdo?" (acá es donde una captura de contacto para el próximo drop resolvería la objeción)

**Resolver mediante:** contador de stock real, mensajes cortos y directos, transparencia sobre que no hay reposición — nunca un FAQ largo o un tono corporativo que rompa la actitud de la marca.

### 7. Puntos de Fricción

**Buscar:**
- CTAs que no llevan a ningún lado (`href="#"` en "IR A LA TIENDA" / "VER TODO")
- Carrito que no hace nada (CART (0) estático)
- Próximos pasos poco claros después de "querer comprar"
- Problemas de experiencia mobile (la marca se consume mucho desde el celular)
- Tiempos de carga largos por imágenes pesadas sin optimizar

---

## Herramientas

| Herramienta | Invocación | Salida |
|---|---|---|
| Auditoría de conversión | `python3 scripts/conversion_audit.py --file CRUDO-Landing.html` (o `--url https://crudo-landing-kappa.vercel.app`; `--json` para pipelines) | Escaneo mecánico de señales de conversión: presencia/cantidad de CTAs, peso de formularios, prueba social, elementos de confianza — con un puntaje |

Correrla antes del análisis manual del framework; su puntaje ancla la auditoría y sus alertas alimentan la lista de Quick Wins.

---

## Formato de Salida

Abrir con el puntaje de `conversion_audit.py`, después estructurar las recomendaciones como:

### Quick Wins (Implementar Ya)
Cambios fáciles con impacto probable inmediato (ej.: conectar los CTAs placeholder, agregar captura de contacto para el próximo drop).

### Cambios de Alto Impacto (Priorizar)
Cambios más grandes que requieren más esfuerzo pero mejoran significativamente la conversión (ej.: conectar checkout real, instalar analytics).

### Ideas para Testear
Hipótesis que conviene testear con A/B en vez de asumir (ej.: texto del CTA, ubicación del contador de stock).

### Alternativas de Copy
Para los elementos clave (títulos, CTAs), dar 2-3 alternativas con justificación.

---

## Frameworks Específicos por Tipo de Página

### CRO de Home/Landing (aplica directo a CRUDO)
- Posicionamiento claro para visitantes fríos que llegan desde Instagram
- Camino rápido hacia la conversión principal: comprar
- Manejar tanto a quien "ya quiere comprar" como a quien "todavía está mirando"

### CRO de Sección Drop/Urgencia
- El match de mensaje con la fuente de tráfico es crítico (si vino por una story del drop, la sección tiene que confirmar esa promesa)
- Un solo CTA, sin navegación que distraiga
- Argumento completo (qué es, cuánto queda, cuándo se agota) en una sola sección

### CRO de Colección/Grilla de Producto
- Comparación clara entre las prendas disponibles
- Indicación de qué queda menos stock
- Resolver la ansiedad de "¿me quedará bien / vale la pena?"

### CRO de Sección Quiénes Somos
- Conecta actitud de marca con beneficio para quien compra
- Casos de uso: mostrar la prenda puesta, en contexto de calle
- Camino claro de vuelta a comprar (no dejar la sección como punto muerto)

---

## Ideas de Experimentos

Al recomendar experimentos, considerar tests para:
- Hero (título, foto, CTA — ej.: "NUEVO DROP" vs. variantes con cantidad de piezas en el título)
- Ubicación y formato del contador de stock/urgencia
- Presentación del precio (con o sin comparación, con o sin edición numerada destacada)
- Captura de contacto para el próximo drop (popup vs. sección fija)
- Navegación y experiencia mobile (tráfico mayormente celular)

---

## Preguntas Específicas de la Tarea

1. ¿Cuál es la tasa de conversión actual y el objetivo? (hoy no hay analytics instalado — puede ser el primer punto a resolver)
2. ¿De dónde viene el tráfico?
3. ¿Cómo sigue el proceso de compra después de esta página? (hoy: no hay tienda conectada)
4. ¿Hay research de usuarios, heatmaps o grabaciones de sesión?
5. ¿Qué se probó ya?

---

## Skills Relacionadas

- **signup-flow-cro** — CUÁNDO: la página convierte bien pero se pierden usuarios en un flujo de registro posterior. CUÁNDO NO: no aplica si el problema es la página en sí (hoy es el caso — arreglar la página primero).
- **form-cro** — CUÁNDO: la página tiene un formulario de captura de contacto (ej.: lista de espera del próximo drop) que es en sí mismo un punto de conversión. CUÁNDO NO: no usar para flujos de registro/cuenta.
- **popup-cro** — CUÁNDO: se está evaluando un popup o modal de intención de salida como capa extra de conversión (ej.: capturar contacto de quien no compra). CUÁNDO NO: no recurrir a popups antes de arreglar los problemas centrales de la página (CTAs rotos).
- **copywriting** — CUÁNDO: la página necesita una revisión de copy completa, no solo ajustes de CTA; hay que reconstruir la arquitectura de mensaje desde la propuesta de valor. CUÁNDO NO: no invocar copywriting para iteraciones menores de título o botón.
- **ab-test-setup** — CUÁNDO: las recomendaciones ya están listas y hace falta un plan de experimento estructurado para validar cambios sin adivinar. CUÁNDO NO: no usar antes de tener una hipótesis clara del análisis CRO.
- **onboarding-cro** — CUÁNDO: el problema real es la activación post-conversión y la página ya convierte de forma aceptable. CUÁNDO NO: no saltar a esto antes de confirmar que la tasa de conversión de la página es aceptable (hoy no aplica: CRUDO no tiene onboarding post-compra).
- **marketing-context** — CUÁNDO: siempre leer `.claude/product-marketing-context.md` primero para entender ICP, mensaje y fuentes de tráfico antes de evaluar la página. CUÁNDO NO: omitir si el usuario ya compartió todo el contexto relevante directamente.

---

## Comunicación

Toda salida de page CRO sigue este estándar de calidad:
- Las recomendaciones siempre se organizan como **Quick Wins → Alto Impacto → Ideas para Testear** — nunca una lista plana
- Cada recomendación incluye una justificación breve ligada a la dimensión del framework CRO que aborda
- Las alternativas de copy se dan en sets de 2-3 con el razonamiento de cada variante
- El framework específico por tipo de página (home, drop, colección, etc.) se aplica explícitamente — nada de consejos genéricos
- Nunca recomendar A/B testing como sustituto de arreglos obvios (como los CTAs placeholder); señalar qué arreglar directo vs. qué testear
- No prescribir layout sin reconocer la fuente de tráfico y el contexto de audiencia

---

## Alertas Proactivas

Mostrar recomendaciones de page-cro automáticamente cuando:

1. **"Esta página no convierte"** — cualquier mención de baja conversión, bajo rendimiento o alto rebote activa de inmediato el framework de análisis CRO.
2. **Se está construyendo una landing/sección nueva** — cuando las skills de copywriting o diseño están activas y se está creando una página de marketing, ofrecer proactivamente una revisión CRO antes del lanzamiento.
3. **Se menciona tráfico pago o campaña puntual** — si el usuario describe correr una campaña (ej.: Instagram Ads) hacia la página, marcar de inmediato el match de mensaje y las mejores prácticas de CTA único.
4. **Se discute el precio de las prendas** — cualquier conversación de estrategia de precio o packaging; recomendar proactivamente una revisión CRO de la sección de precios junto con el trabajo de posicionamiento.
5. **Se revisan resultados de un A/B test** — cuando la skill ab-test-setup muestra resultados de test, ofrecer un análisis page-cro para generar la próxima ronda de hipótesis.

---

## Artefactos de Salida

| Artefacto | Formato | Descripción |
|----------|--------|-------------|
| Resumen de Auditoría CRO | Secciones en Markdown | Análisis en las 7 dimensiones del framework con severidad de cada problema |
| Lista de Quick Wins | Lista con viñetas | ≤5 cambios implementables ya, con impacto esperado |
| Recomendaciones de Alto Impacto | Lista estructurada | Cada una con justificación, esfuerzo estimado y métrica de éxito |
| Alternativas de Copy | Tabla comparativa | 2-3 variantes por elemento clave (título, CTA, subtítulo) con razonamiento |
| Hipótesis de A/B Test | Tabla | Hipótesis × descripción de variante × métrica de éxito × prioridad |
