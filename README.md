# Handoff: CRUDO — Landing Page

## Overview
Landing page for CRUDO, an Argentine streetwear brand (limited-edition drops). Single-page scrolling site: hero impact, current drop urgency, product collection, brand manifesto, purchase/follow CTAs, footer.

## About the Design Files
The bundled file (`CRUDO-Landing.dc.html`) is a **design reference built in HTML** — a prototype showing the intended look, layout, copy, and interactions, not production code to copy verbatim. The task is to **recreate this design in the target codebase's existing environment** (React, Vue, plain HTML/CSS, etc.) using its established patterns and libraries — or, if no environment exists yet, choose the most appropriate framework and implement it there.

## Fidelity
**High-fidelity.** Colors, typography, spacing, and copy are final per the brand manual. Recreate pixel-perfectly.

## Screenshots
Full-page reference captures are in `screenshots/`, one per section, in scroll order:
1. `01-hero.png` — Hero + header
2. `02-drop.png` — Drop actual (urgency)
3. `03-shop.png` — Colección (product grid)
4. `04-somos.png` — Quiénes somos (manifesto)
5. `05-seguinos.png` — Comprá / Seguinos
6. `06-footer.png` — Footer

## Screens / Views

### 1. Header (overlaid on hero, transparent)
- 3-column layout: logo left, nav centered, cart indicator right.
- Logo: `logo-negativo.png` (hueso-on-black), height 63px, `width:auto`, `object-fit:contain`.
- Grid: `grid-template-columns: 1fr auto 1fr`, `align-items: center`, logo `justify-self:start`, nav `justify-self:center`, cart `justify-self:end`.
- Nav links (in this order): SHOP → `#shop` (Colección section), DROPS → `#drop` (Drop actual section), ABOUT → `#somos` (Quiénes somos), CONTACT → `#seguinos` (Comprá/Seguinos). Font Inter, 14px, weight 600, uppercase via source text (not CSS transform), letter-spacing 0.08em, color Hueso `#EDEDED`, gap between links 40px. Hover: color transitions to Volt `#D6FF00` over 0.2s ease.
- Cart indicator: flex row, gap 10px, "CART (0)" in Roboto Mono 13px letter-spacing 0.05em color Hueso, plus a 10×10px solid Volt circle (`border-radius:50%`).
- Position: `position:absolute; top:0; left:0; right:0; z-index:3;` over the hero image (transparent background — no separate bar), padding 28px 48px.

### 2. Hero
- Section: `min-height:92vh`, `display:flex; align-items:flex-end;`, bottom padding 80px (content sits low, anchored to bottom third).
- Background photo: `hero-photo-crop.png`, `position:absolute; inset:0;`, `object-fit:cover`, `object-position:70% center` — man crouching against a graffiti'd concrete wall, high-contrast B&W-leaning grade with a Volt "CRUDO" tag sprayed on the wall.
- Overlay: `position:absolute; inset:0; z-index:1;` gradient `linear-gradient(90deg, rgba(14,14,14,.85) 0%, rgba(14,14,14,.35) 55%, rgba(14,14,14,.15) 100%)` — darkens the left/text side, lets the photo breathe on the right.
- Content wrapper: `z-index:2`, `max-width:900px`, `padding:0 48px`.
- Headline "NUEVO DROP" (two lines via `<br>`): font Anton, `font-size:min(11vw,140px)`, `line-height:0.88`, uppercase (literal caps in source text, no `text-transform`), color Hueso `#EDEDED`, `letter-spacing:0.01em`, `margin:0`.
- "EDICIÓN LIMITADA." — Anton 26px uppercase, color Volt `#D6FF00`, `margin:24px 0 4px`.
- "Cuando se agota, no vuelve." — Anton 26px uppercase, color Hueso, `margin:0 0 32px`.
- CTA "VER DROPS": `<a>` styled as button, `display:inline-block`, background Volt, text color Negro `#0E0E0E`, font Anton 18px uppercase, `letter-spacing:0.05em`, `padding:18px 40px`, no border-radius. Hover: `transform:scale(1.05)` over 0.25s ease. Links to `#drop`.
- Bottom-left detail: `position:absolute; left:48px; bottom:28px; z-index:2;` flex row gap 10px, Roboto Mono 15px, Hueso — reads "DROP_01" + Volt "/" + "150" (total pieces across both SKUs this drop; keep in sync with the Colección/Drop-actual numbers if edited).
- Entrance animation (runs once on page load, not scroll-triggered): headline, "EDICIÓN LIMITADA.", "Cuando se agota…", and the CTA each get `animation: fadeUp 0.9s ease both` with staggered delays 0s / 0.15s / 0.25s / 0.35s. Keyframes: `@keyframes fadeUp { from { opacity:0; transform:translateY(28px); } to { opacity:1; transform:translateY(0); } }`.

### 3. Drop actual (urgency), id `drop`
- Section padding: 120px 48px. `position:relative; overflow:hidden;` to contain the texture/vignette layers.
- Layer 1 (z-index 0): `tela-indumentaria.png` (dark navy-black woven fabric close-up) as a full-bleed `position:absolute; inset:0;` image, `object-fit:cover`, `opacity:0.35`.
- Layer 2 (z-index 1): `radial-gradient(ellipse at 30% 20%, rgba(28,28,28,0.2) 0%, rgba(14,14,14,0.85) 75%)` over the texture, to keep it subtle and keep contrast for text.
- Content (z-index 2, `id="drop-reveal"` in the source — the scroll-reveal target): `max-width:1200px; margin:0 auto;` two-column grid `1.1fr / 1fr`, `gap:64px`, `align-items:center`.
- Left column:
  - Eyebrow "Stock en vivo" — Roboto Mono 14px, color Rojo Alerta `#FF3B2F`, `letter-spacing:0.1em`, uppercase, `margin:0 0 20px`.
  - Headline "DROP_01 YA ESTÁ AFUERA" (two lines) — Anton, `font-size:clamp(40px,6vw,72px)`, uppercase, Hueso, `line-height:0.95`, `margin:0 0 24px`.
  - Body copy: "150 piezas entre buzos y gorras. Ni una más. Cuando se acaban, se acabaron — no hay reposición, no hay "vuelve el mes que viene"." — Inter 18px, color Gris Humo `#8A8A8A`, `max-width:480px`, `line-height:1.6`, `margin:0 0 32px`.
  - "Lanzado: 12/07/2026" — Roboto Mono 15px, Gris Humo.
- Right column (stock card): background Negro `#0E0E0E`, `border:1px solid #2A2A2A`, `padding:48px`.
  - "DISPONIBLES" label — mono 14px, Gris Humo, `letter-spacing:0.05em`, `margin:0 0 12px`.
  - Counter "42 / 150" — the "42" in Anton 64px Hueso, the "/ 150" part in Anton 32px Gris Humo, same line, `margin:0 0 8px`.
  - Progress bar: track `height:6px; background:#2A2A2A; width:100%; margin-bottom:24px;`, fill `height:100%; width:28%; background:#FF3B2F;` (28% ≈ 42/150 remaining — keep this percentage in sync with the counter numbers).
  - Urgency line "No duermas cocodrilo, que vuela y sos cartera" — mono 13px, Rojo Alerta, uppercase, `letter-spacing:0.05em`.
- Scroll-reveal: the whole `#drop-reveal` content block starts at `opacity:0; transform:translateY(40px);` and animates to `opacity:1; transform:translateY(0);` over `0.9s cubic-bezier(.2,.7,.3,1)` (both opacity and transform) the first time it's ≥15% in the viewport (`IntersectionObserver`, `threshold:0.15`, unobserved after firing — animates once, not on every scroll pass).

### 4. Colección, id `shop`
- Background Negro, section padding 120px 48px. Inner wrapper `max-width:1400px; margin:0 auto;` — this wrapper (`id="shop-reveal"`) is the scroll-reveal target (same fade-up mechanics as the Drop section).
- Header row: `display:flex; justify-content:space-between; align-items:flex-end; margin-bottom:56px; flex-wrap:wrap; gap:24px;` — "COLECCIÓN" (Anton, `clamp(40px,5vw,64px)`, uppercase, Hueso) on the left, "DROP_01 — 2 PRENDAS" (Roboto Mono 14px, Gris Humo) on the right.
- Grid: `repeat(auto-fit, minmax(340px,1fr))`, `gap:32px`. Exactly **two** product cards for this drop — do not add placeholder/extra products:
  1. **Buzo CRUDO OG** — image `producto-1.png` (black oversized hoodie, cracked-concrete CRUDO chest print, "SIN FILTRO. SIN POSES. SIN VUELTAS." tagline beneath in Volt, laid flat on a distressed grey concrete backdrop) — price **$55.000** — edition tag **01/100**.
  2. **Gorra CRUDO OG** — image `producto-2.png` (black dad cap, same cracked-texture CRUDO embroidery + Volt tagline, shot on a concrete ledge with spray-painted Volt "CRUDO" graffiti in the background) — price **$15.000** — edition tag **01/50**.
- Card anatomy: `background:#1C1C1C` (Asfalto), image wrapped in `overflow:hidden` div, image itself `width:100%; aspect-ratio:1/1; object-fit:cover; display:block;` with `transition:transform 0.3s ease, filter 0.3s ease;` and hover state `transform:scale(1.04); filter:brightness(1.1);`. Below the image, `padding:24px`: a row (`display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;`) with the product name (Inter 16px/600, Hueso) on the left and the edition tag (Roboto Mono 13px, Volt) on the right, then the price on its own line (Roboto Mono 18px, Hueso).
- "VER TODO" button: centered below the grid (`margin-top:56px`), Volt background, Negro text, Anton 16px uppercase, `letter-spacing:0.05em`, `padding:16px 44px`, hover `transform:scale(1.05)` over 0.25s. Currently `href="#"` — wire to the real catalog/collection route.

### 5. Quiénes somos, id `somos`
- Section: `position:relative; padding:140px 48px; min-height:80vh; display:flex; align-items:center;`.
- Background: `gente-en-la-calle.png` full-bleed (`position:absolute; inset:0; object-fit:cover;`) — four people from behind in black CRUDO hoodies/tees on a street, walking away from camera past graffiti'd roll-down shutters.
- Overlay: `linear-gradient(90deg, #0E0E0E 20%, rgba(14,14,14,0.55) 60%, rgba(14,14,14,0.15) 100%)` — solid Negro on the left third for text legibility, fading to reveal the photo on the right.
- Content (`id="somos-reveal"`, the scroll-reveal target): `max-width:640px`.
  - Eyebrow "Quiénes somos" — Roboto Mono 14px, Volt, uppercase, `letter-spacing:0.1em`, `margin:0 0 24px`.
  - Headline "SOMOS DE LA CALLE PARA LA CALLE." (line break after "CALLE") — Anton, `clamp(36px,5vw,56px)`, uppercase, `line-height:1.05`, Hueso, `margin:0 0 28px`.
  - Paragraph 1 (Hueso, 19px, `line-height:1.7`): "No diseñamos para pasar desapercibidos. CRUDO existe porque la calle nos hizo así: sin filtro, sin careta, sin pedir permiso."
  - Paragraph 2 (Gris Humo, 19px, `line-height:1.7`): "Tirada limitada. Siempre. Si no incomoda un poco, no es CRUDO."
- Scroll-reveal: identical mechanics to the Drop section (fade up, 0.9s cubic-bezier(.2,.7,.3,1), fires once at 15% visibility).

### 6. Comprá / Seguiños, id `seguinos`
- Section: `position:relative; padding:64px 48px; background:#1C1C1C; overflow:hidden;` (shorter vertical padding than other sections — this one is meant to feel snug/action-oriented, not another full "chapter").
- Same texture treatment as the Drop section: `tela-indumentaria.png` at 35% opacity (z-index 0) + `radial-gradient(ellipse at 70% 80%, rgba(28,28,28,0.2) 0%, rgba(14,14,14,0.85) 75%)` vignette (z-index 1) — note the gradient's focal point is bottom-right here vs. top-left in the Drop section, for visual variety.
- Content (`id="seguinos-reveal"`, scroll-reveal target, z-index 2): `max-width:1200px; margin:0 auto;` two-column grid `1fr / 1fr`, `gap:32px`.
- Card 1 — COMPRÁ: `background:#0E0E0E; padding:56px 48px;`. "01" index (mono 14px, Gris Humo, `letter-spacing:0.1em`, `margin:0 0 16px`). "COMPRÁ" (Anton, `clamp(32px,4vw,48px)`, uppercase, Hueso, `margin:0 0 20px`). Body: "Entrá a la tienda. Lo que ves es lo que hay — sin reposición." (Inter 16px, Gris Humo, `line-height:1.6`, `margin:0 0 32px`). Button "IR A LA TIENDA": Volt bg, Negro text, Anton 16px uppercase, `padding:16px 40px`, hover `scale(1.05)`. **`href="#"` placeholder — no external store exists yet; wire to the real shop URL when available.**
- Card 2 — SEGUINOS: same card shell. "02" index. "SEGUINOS" heading. Body: "Mirá el próximo drop antes que nadie." Instagram link: `display:inline-flex; align-items:center; gap:12px;`, a 10×10px solid Volt square bullet + "@crudo_arg" in Roboto Mono 20px Hueso, `href="https://instagram.com/crudo_arg"`, `target="_blank"`.
- Scroll-reveal: same fade-up mechanics as the other sections.

### 7. Footer
- `background:#0E0E0E`, `border-top:1px solid #1C1C1C`, `padding:56px 48px 40px`. Not part of the scroll-reveal system — always visible immediately (footers shouldn't feel like they're "arriving").
- Inner wrapper `max-width:1200px; margin:0 auto;`.
- Top row: `display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:24px; margin-bottom:40px;` containing:
  - Logo `logo-negativo.png`, `height:48px`, `width:auto`.
  - Nav repeat: SHOP (`#shop`) / DROPS (`#drop`) / ABOUT (`#somos`) / CONTACT (`#seguinos`) — `display:flex; gap:32px; flex-wrap:wrap;`, each link Inter 13px/600, Gris Humo, `letter-spacing:0.06em` (no hover state currently defined on these — consider adding the same Volt hover as the header nav for consistency).
  - "@CRUDO_ARG" — same Gris Humo/13px/600 styling, links to `https://instagram.com/crudo_arg`.
- Bottom line: "SIN FILTRO. SIN POSES. SIN VUELTAS." — Roboto Mono 12px, Gris Humo, `letter-spacing:0.08em`, centered (`text-align:center`), `margin:0`.

## Interactions & Behavior
- All nav links are in-page anchor scrolls (`#shop`, `#drop`, `#somos`, `#seguinos`).
- Hero content animates in once on load (CSS `@keyframes fadeUp`).
- Section content (`#drop-reveal`, `#shop-reveal`, `#somos-reveal`, `#seguinos-reveal`) fades/slides in once when it enters the viewport (`IntersectionObserver`, threshold 0.15, unobserve after firing).
- Product images and all CTA buttons scale/brighten slightly on hover (0.25–0.3s ease).
- Nav links change from Hueso to Volt on hover.
- "IR A LA TIENDA" and "VER TODO" are placeholder links (`href="#"`) — no external store yet; wire up when the real shop URL exists.
- No cart logic implemented — "CART (0)" is static UI only.

## State Management
No app state beyond the one-shot scroll-reveal flags (handled via DOM IntersectionObserver, not component state, in the source prototype). A React rebuild can model reveal-per-section as boolean state driven by `IntersectionObserver` refs.

## Design Tokens

### Colors (exact — from brand manual, do not approximate)
- Negro `#0E0E0E` — dominant background
- Asfalto `#1C1C1C` — secondary blocks/cards
- Hueso `#EDEDED` — primary text
- Volt `#D6FF00` — accent, CTAs/prices/tags ONLY, never fill
- Gris Humo `#8A8A8A` — secondary text
- Rojo Alerta `#FF3B2F` — urgency/stock warnings only

### Typography
- Headlines: **Anton** (uppercase, heavy, condensed)
- Body: **Inter** (400–700)
- Labels/prices/codes: **Roboto Mono** (stand-in for Courier)
- Google Fonts import: `Anton`, `Inter:wght@400;500;600;700`, `Roboto Mono:wght@400;500;700`

### Spacing
- Section vertical padding: 64–140px depending on section weight
- Horizontal page padding: 48px
- Card padding: 24–56px
- Grid gaps: 32–64px

### Other
- No border-radius anywhere (hard-edged, brand is deliberately un-rounded)
- Card borders: 1px solid `#2A2A2A` where used
- Button shape: rectangular, no radius

## Assets
- `logo-negativo.png` — CRUDO wordmark, hueso on black (header + footer)
- `logo-volt-sobre-negro.png` — CRUDO wordmark, volt on black (available, not currently placed — reserve for a "brand shouts" moment if added later)
- `logo-principal.png` — CRUDO wordmark, black on white (for light backgrounds, not currently used)
- `hero-photo-crop.png` — cropped hero photo (cropped from the client-supplied `herp-imagen-principal.png` mockup to isolate the photograph only, since the original file had UI baked in)
- `gente-en-la-calle.png` — group lifestyle photo, Quiénes somos section
- `producto-1.png` — Buzo CRUDO OG product shot
- `producto-2.png` — Gorra CRUDO OG product shot
- `tela-indumentaria.png` — fabric texture, used as a subtle low-opacity background layer in the Drop and Comprá/Seguinos sections

## Files
- `CRUDO-Landing.dc.html` — full design source (single-file HTML/inline-styles prototype)
- `screenshots/` — one PNG per section (see Screenshots above)
- `assets/` — all image assets listed above, at original resolution
