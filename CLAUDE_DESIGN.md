# Prompt para Claude Design — Landing CRUDO

> Cómo usar este archivo: copiá todo el bloque de "PROMPT" de abajo y pegalo en Claude Design. Las secciones de arriba son para que vos entiendas las decisiones que tomé (por si te preguntan en el video final por qué elegiste esto).

---

## Por qué esta estructura (para tu defensa del proyecto)

El manual pide 3 cosas no negociables: **impacto inmediato**, **prenda como protagonista** y **urgencia de drop**. Por eso la landing sigue este orden:

1. **Hero** → el golpe inicial, lo primero que ve cualquiera.
2. **Drop actual** → la urgencia ("cuando se agota, no vuelve") va temprano, no al final.
3. **Colección / grilla de productos** → las prendas protagonistas, fotos grandes.
4. **Quiénes somos** → la actitud y el manifiesto, sin vueltas.
5. **Cómo comprar / seguir** → CTA final: tienda + Instagram.
6. **Footer** → mínimo, solo lo esencial.

Nada de secciones tibias tipo "testimonios" o "newsletter" genérico — no está en el brief y le bajaría la actitud.

---

## PROMPT (copiar y pegar en Claude Design)

```
Quiero diseñar desde cero la landing page de CRUDO, una marca de streetwear
argentina. Trabajemos primero el Design System y después cada sección.

## 1. MARCA Y ACTITUD

CRUDO es ropa para los que no piden permiso. Prendas de edición limitada,
hechas desde la calle y para la calle. No es una marca más de ropa, es una
actitud: fuerza, calle, personalidad. Si no incomoda un poco, no es CRUDO.
Nada tibio, nada genérico, nada que se confunda con cualquier otra marca.

Público: pibes y pibas de 18 a 30 que se visten para expresar quiénes son,
no para pasar desapercibidos.

## 2. DESIGN SYSTEM (configurar esto ANTES de diseñar cualquier pantalla)

Colores (usar EXACTOS, no aproximados):
- Negro #0E0E0E — dominante, fondo principal
- Asfalto #1C1C1C — secundario, bloques y tarjetas
- Hueso #EDEDED — texto principal, contraste
- Volt #D6FF00 — acento clave, SOLO en botones y detalles que quiero que
  se miren (CTAs, precios, tags). Nunca de relleno.
- Gris Humo #8A8A8A — textos secundarios
- Rojo Alerta #FF3B2F — reservado solo para avisos de drop / urgencia
  ("agotado", "últimas unidades")

Regla de uso del color: negro domina todo, hueso para leer, volt usado con
mucha moderación para que siga gritando cuando aparece.

Tipografía:
- Titulares: una sans pesada, condensada y en mayúsculas, tipo Anton o
  Archivo Black. Grande, con actitud, que ocupe espacio.
- Textos de cuerpo: sans limpia y neutra, tipo Inter o Helvetica, para que
  se lea bien.
- Detalles tipo etiqueta/código (precios, "DROP_01", "SOLD OUT"): tipografía
  monoespaciada, tipo Courier.

Logo: viene en 3 versiones — hueso sobre negro (default), volt sobre negro
(para cuando la marca "tiene que gritar"), y negro sobre fondos claros.
No deformar, no achicar de más, dejarle aire alrededor.

Fotografía: alto contraste, sombras marcadas, ambiente urbano (paredes,
calle, cemento). Poses reales, no de catálogo careta. La prenda siempre
protagonista, con espacio para fotos grandes a pantalla completa.

Tono de voz (esto tiene que sentirse en cada texto de la web): corto,
directo, con actitud, como habla la calle. Nada de marketing acartonado.
Ejemplo de referencia: "Nuevo drop. Tirada limitada. Cuando vuela, voló."
Nunca: "Te invitamos a descubrir nuestra nueva y exclusiva colección..."

## 3. ESTRUCTURA DE LA LANDING (en este orden)

### Header
Logo CRUDO (versión hueso sobre negro) a la izquierda. Nav simple: SHOP,
DROPS, ABOUT, CONTACT. Ícono/link de carrito a la derecha. Fondo negro,
minimalista, no le robe protagonismo al hero.

### 1. Hero (foto principal / impacto inicial)
Pantalla completa. Foto de lifestyle en blanco y negro/alto contraste como
fondo (persona con prenda CRUDO en ambiente urbano). Título gigante en
titular pesado: "NUEVO DROP". Debajo, en volt: "EDICIÓN LIMITADA." y en
hueso: "Cuando se agota, no vuelve." Botón CTA en volt: "VER DROPS". Un
detalle mono abajo a la izquierda tipo "DROP_01 / 25" que refuerza la
escasez desde el primer segundo.

### 2. Drop actual (urgencia)
Sección que muestra el drop vigente como algo que se agota. Contador o
indicador de stock restante (ej: "18/100 disponibles"), fecha del drop,
y un texto corto reforzando la idea de que esto no vuelve. Fondo asfalto
para diferenciarse del negro del hero.

### 3. Colección (grilla de productos)
Grilla de 3-4 columnas con fotos grandes de producto (buzo, remera, gorra).
Cada tarjeta: foto de producto, nombre corto, precio en tipografía mono,
tag de edición si corresponde (ej: "01/100"). Hover con leve intensidad
(zoom o cambio de brillo), nada de animaciones tibias. Botón "VER TODO"
al final en volt.

### 4. Quiénes somos (manifiesto de marca)
Sección con fondo negro y foto lifestyle de grupo (varios pibes con
prendas CRUDO en la calle). Texto corto tipo manifiesto: quiénes son,
de dónde vienen, por qué existen. Usar frases cortas, contundentes, no
un párrafo largo explicando la historia de la empresa. Foco en actitud,
autenticidad y escasez (los 3 pilares del manual).

### 5. Cómo comprar / seguir (CTA final)
Dos bloques lado a lado o uno arriba del otro:
- "COMPRÁ" con botón grande en volt que linkea a la tienda externa.
- "SEGUINOS" con el link de Instagram destacado (es el canal central
  de la marca), ícono simple, texto tipo "@crudo — mirá el próximo drop
  antes que nadie".

### Footer
Minimalista: logo chico, links de navegación repetidos, redes sociales,
y un texto mono chico tipo "SIN FILTRO. SIN POSES. SIN VUELTAS." Fondo
negro, texto hueso/gris humo, sin relleno innecesario.

## 4. CHEQUEO ANTES DE TERMINAR
- ¿Se siente la energía de la marca apenas entrás, sin leer nada?
- ¿El texto suena a calle o suena a banco? (tiene que sonar a calle)
- ¿El volt aparece poco pero fuerte, no de relleno?
- ¿Las prendas tienen espacio grande y protagónico?
- ¿Se entiende la urgencia de "edición limitada" en los primeros segundos?

Empecemos configurando el Design System con estos colores y tipografías
antes de generar ninguna pantalla.
```

---

## Después de esto (recordatorio para vos, no para Claude Design)

1. Iterá visualmente sobre cada sección (apuntá, comentá, ajustá) antes de pasar a la siguiente.
2. Cuando el diseño te cierre, hacé el **handoff a Claude Code**.
3. Revisá que colores, tipografías y estructura no se rompan en el pasaje.
4. **Deploy** + probar en mobile (streetwear se mira mucho desde el celular).
5. Grabar el video corto explicando tus decisiones.
