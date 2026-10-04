# Handoff: Presentación de soporte para usuarios nuevos

## Overview
Presentación interactiva (9 láminas, 1920×1080) que explica a usuarios nuevos del grupo CNA cómo pedir soporte: plan de puesta en marcha de 3 días, la regla "sin ticket no hay atención", cómo crear un ticket en el Portal Interno del grupo (https://portal-interno.cnagro.cl/), preguntas frecuentes y reglas de cierre.

## About the Design Files
Los archivos de esta carpeta son **referencias de diseño creadas en HTML**: prototipos que muestran el aspecto y comportamiento esperado, no código de producción para copiar tal cual. La tarea es **recrearlos en el entorno del proyecto destino** (React, Vue, Reveal.js, Next.js, etc.) usando sus patrones. Si no existe proyecto, elegir el framework más adecuado (sugerido: React + Vite, o una página estática con un shell de slides).

Para ver el prototipo: abrir `Soporte-Presentacion.dc.html` en un navegador servido localmente (`npx serve .`). Depende de `support.js` (runtime) y `deck-stage.js` (shell de slides: escalado, navegación con teclado, miniaturas, impresión).

## Fidelity
**Alta fidelidad.** Colores, tipografía, espaciados y textos son finales.

## Slides
Lienzo fijo 1920×1080, escalado para ajustarse a la ventana. Navegación con ← → / espacio.

1. **Portada** — fondo verde bosque `#1f3527`, padding 120/140. Título "Modelo de soporte" 150px/600, subtítulo 40px `#dbe5d5`. Al pie, 3 equipos con cuadrado de color 18px: Netsus `oklch(0.65 0.13 230)`, ITSPACKS `oklch(0.65 0.13 60)`, Desarrollo y Proyectos Holding `oklch(0.65 0.13 310)`.
2. **Plan 3 días** — fondo crema `#f5f1e6`. Título "Así comenzamos: 3 días" 80px. Dos tarjetas en grid 1fr 1fr, gap 32, radio 20, padding 48:
   - "DÍAS 1 Y 2 · PRESENCIAL" (blanca, borde superior 8px azul `oklch(0.6 0.13 230)`): "Puesta en marcha en tienda": personal técnico en tienda que apoya (1) la configuración de computadores con la información respaldada, incluido Office, y (2) la configuración de la red e impresoras. Chips de tiendas: Santiago, Coquimbo, Lautaro, San Fernando, Chillán.
   - "DÍA 3 · TODAS LAS TIENDAS" (verde `#1f3527`, borde superior verde `oklch(0.72 0.15 150)`): "Operación por tickets" y el link portal-interno.cnagro.cl.
3. **Regla principal** — fondo trigo `oklch(0.86 0.09 88)`, texto `#1f3527`. Etiqueta "La regla más importante", titular "Sin ticket, no podemos atenderte." 180px/700, párrafo 40px y un recuadro verde con la URL.
4. **¿Quién atiende tu caso?** — fondo crema, subtítulo "Tenemos un equipo preparado para apoyar tu trabajo.", 4 tarjetas en grid repeat(4,1fr) con borde superior del color del equipo: Netsus (accesos, contraseñas, equipos, dudas de uso), ITSPACKS (JD Edwards), Desarrollo y Proyectos Holding (mejoras y proyectos) y "¿No sabes cuál?" → Netsus reclasifica (verde CNA).
5. **Cómo crear tu ticket** — 5 tarjetas en una fila (grid repeat(5,1fr)), con círculo numerado verde de 64px, título 36px y descripción 26px. El paso 1 muestra la URL en un recuadro verde claro, partida en "portal-interno" / ".cnagro.cl".
6. **Así se completa el formulario** — captura `assets/nuevo-ticket.png` a 1640×684 con 9 hotspots numerados (círculos de 46px). Al hacer clic en uno se resalta y la franja oscura inferior muestra el título y la explicación del campo. Coordenadas en % sobre la imagen (left, top):
   1 Nuevo Ticket (8.2, 19.1) · 2 Área de soporte (9.6, 34.6) · 3 Categoría (31.4, 34.6) · 4 Tipo (53.2, 34.6) · 5 Prioridad (75.0, 34.6) · 6 Título y teléfono (9.6, 49.3) · 7 Descripción (9.6, 58) · 8 Adjuntos (9.6, 75.3) · 9 Crear Ticket (9.6, 93).
   Textos: Categoría = Incidente o Requerimiento. Tipo = Celular, Impresora, JD Edwards, Notebook, Office 365, Pantalla, Portal Agrocompra, Portal Cobranza, Portal Interno, Portal Smart, Power BI, SAP. Adjuntos = JPG, PNG, PDF, Word, Excel, máximo 20 MB.
7. **En qué va tu ticket** — fondo verde, 5 tarjetas `#28432f` con los estados Nuevo · Asignado · En atención · Resuelto · Cerrado. "Resuelto" va en trigo con la etiqueta "Tu turno" (el usuario debe confirmar). Al pie, la nota de reapertura.
8. **Preguntas frecuentes** — grid 860px | 1fr. A la izquierda, una lista de 7 preguntas en botones. A la derecha, un panel verde oscuro con la respuesta y la URL fija al pie. La pregunta activa lleva un borde verde de 3px.
9. **4 cosas para recordar** — fondo verde, grid 2×2: Siempre crea un ticket · Elige bien la categoría · ¿Te equivocaste? No pasa nada (Netsus reclasifica) · Guarda tu número de ticket. Al pie, una franja trigo con la URL del portal.

Los textos exactos de cada lámina están en el HTML: el texto fijo en el template y las listas (pasos, hotspots, FAQ, reglas) en `renderVals()` dentro del `<script>`.

## Interactions & Behavior
- Navegación entre láminas: teclado, panel de miniaturas, `deck.goTo(n)`.
- Lámina 6: estado `spot` (índice del hotspot activo, por defecto 0). Transición de 0.2s en el fondo y la sombra.
- Lámina 8: estado `faq` (índice de la pregunta activa, por defecto 0).
- Los links a la URL abren en una pestaña nueva.
- Impresión/PDF: una página por lámina.

## State Management
Solo estado local de UI: `spot: number` y `faq: number`. No hay carga de datos.

## Design Tokens
- Verde bosque (fondos oscuros): `#1f3527`; fondo de la página `#14241a`; bordes sobre fondo oscuro `#335040`; tarjeta sobre fondo oscuro `#28432f`.
- Crema (fondos claros): `#f5f1e6`; tarjetas `#fff` / `#fbf8f0`; bordes `#e4dccb`, `#d6ccb6`.
- Texto: `#1f3527` (tinta), `#4d473c`, `#6f6756` (secundario); sobre fondo oscuro `#dbe5d5`, `#bfcfb9`.
- Acento verde CNA: `oklch(0.6 0.13 150)`, en claro `oklch(0.82 0.12 150)`, en tinta `oklch(0.45 0.12 150)`.
- Trigo: `oklch(0.86 0.09 88)`.
- Tipografía: IBM Plex Sans (400/500/600/700) e IBM Plex Mono (400/500), ambas de Google Fonts. Mínimo 24px en las láminas.
- Radios: 8, 10, 14, 16, 20 y 999 (chips).
- Sombras: `0 16px 40px rgba(20,25,30,.1)` (captura) y `0 0 0 8px oklch(0.6 0.13 150 / .3)` (hotspot activo).

## Assets
- `assets/nuevo-ticket.png` — captura del formulario "Nuevo Ticket" del portal, con los datos del usuario tapados.
- `assets/portal-cna.png` — captura del login del portal (no se usa en la versión actual).

## Files
- `index.html` — versión web responsive (pensada primero para celular) con el mismo contenido. Incluye un formulario de práctica paso a paso (8 pasos, validación en el navegador, nada se envía ni se guarda). En pantallas de 820 px o menos, la presentación redirige aquí (`?deck` fuerza la presentación).
- `Soporte-Presentacion.dc.html` — prototipo completo (template y lógica).
- `deck-stage.js` — web component del shell de slides.
- `support.js` — runtime del prototipo (solo para verlo; no se porta).
