# Lo de Carmi Resto Bar — Landing

## El negocio
- Resto bar de comida casera en Bruselas, Asunción, Paraguay.
- Abre de lunes a viernes, de 8:00 a 13:00.
- Vende: menú del día casero, viandas individuales, combos prepagos (pagás X viandas por adelantado, con descuento frente a comprarlas sueltas) y plan corporativo.
- Los combos también los compran personas individuales, no solo empresas.
- Combos prepagos vigentes: 5 viandas Gs. 125.000, 10 viandas Gs. 250.000, 20 viandas Gs. 450.000. Incluyen bebida gratis todos los días (jugo fresco o gaseosa, se elige al recibir el plato).
- Vianda suelta: entre Gs. 25.000 y 30.000 según el plato (rango, el precio exacto lo da el menú del Sheets).
- Combos: se pagan por QR en el local, transferencia o POS. Se renuevan mensualmente (o lo que dure el combo). Se pueden usar 2 comidas en un mismo día (cuenta como un día menos del combo).
- Formas de pago en general: QR, transferencia; en el local también POS y efectivo.
- Delivery gratis para todos (viandas sueltas, combos y corporativo) si es de la zona; si no, se consulta por WhatsApp. La zona exacta: [COMPLETAR].
- Plan corporativo: NO tiene precios publicados. Depende de la porción, el tamaño y el presupuesto de la empresa, así que se cotiza por WhatsApp. Para cotizar la empresa pasa: nombre de la empresa, cantidad de personas, días por semana, dirección y horario de entrega.
- Los clientes piden y consultan por WhatsApp. Número: 595991878979 (formato wa.me: 595 + número sin el 0 inicial, sin + ni guiones). Es el que está en el HTML (`WA_NUMERO`).
- Instagram: https://www.instagram.com/lodecarmi/
- Google Maps: https://www.google.com/maps/place/LO+DE+CARMI%F0%9F%98%8B+Resto+bar/@-25.2875797,-57.570223,19z/data=!4m6!3m5!1s0x945da9ed57ba5a41:0xd74b41987a4c3f31!8m2!3d-25.2873891!4d-57.5703961!16s%2Fg%2F11vxt2jmy5?entry=ttu&g_ep=EgoyMDI2MTExMC4wIKXMDSoASAFQAw%3D%3D
- Dirección escrita: Bruselas casi Viena, antes de la Contraloría General de la República. Número de casa: [COMPLETAR]

## El proyecto
- Landing en UN solo archivo HTML (HTML + CSS + JS), sin frameworks ni build: `LO DE CARMI/lo-de-carmi-landing2.0.html`.
- Animación: GSAP + ScrollTrigger + Lenis (por CDN).
- Estilos de referencia en `_estilos-design-md/` (DESIGN.md de marcas conocidas). Usarlos como inspiración de sistema, nunca copiar marca, logos ni colores de otra empresa.

### Qué hay hoy en el HTML (diseño "Fogón": oscuro, cálido, Fraunces + DM Sans)
- **Menú del día:** se lee primero de Supabase (función pública `web_menu_hoy()`, proyecto "Sistema de tickets Lo de Carmi resto bar"; constantes `SUPABASE_URL` y `SUPABASE_KEY`, la clave es la publishable, pensada para ir en el navegador). Muestra solo los platos con stock cargado hoy (`daily_stock`) y oculta los agotados. Si Supabase falla o hoy no hay stock cargado, cae al Google Sheets publicado como CSV (hoja 1, `SHEET_CSV_URL`), que se mantiene como respaldo: no borrarlo. Columnas del Sheets: nombre, descripción, precio, guarniciones separadas por "/", imagen (opcional). La primera fila es el encabezado. El dueño lo edita desde el celular. No romper esa conexión.
- **Tarjetas de plato** con selector de guarnición; al elegir una, se rellena el formulario de pedido.
- **Combos prepagos:** los precios vienen de la **hoja 2** del mismo Sheets (columnas `cantidad`, `precio`; primera fila encabezado) vía `PACKS_CSV_URL`. Si esa constante está vacía o la hoja falla, se usan los precios de respaldo (`DEFAULT_PACKS`: 5 = 125.000, 10 = 250.000, 20 = 450.000). **`PACKS_CSV_URL` está vacía todavía: [COMPLETAR] con el link CSV de la hoja 2.**
- **Formulario de pedido** con 3 pestañas (Vianda, Combo prepago, Corporativo) y un ticket "Tu comanda" que cambia según la pestaña. Al enviar arma el mensaje y abre `wa.me` con el texto. Corporativo pide: empresa, cantidad de personas, días por semana, dirección y horario de entrega, sin precios.
- Todos los botones de WhatsApp (header, hero, tarjetas, FAQ, flotante) abren el chat con un mensaje ya armado.
- Secciones: hero, menú, tres formas de comer (combos, local, llevar y delivery), empresas, pedido, FAQ, ubicación, footer.
- **Hero con pizarrón "Hoy se come":** muestra los primeros 4 platos del menú (nombre, línea de puntos, precio) leídos del mismo Sheets de la hoja 1; si el menú falla, muestra un aviso con botón de WhatsApp. No hay foto del hero todavía; cuando haya una real puede ir arriba del pizarrón (comentario en el HTML).
- **Combos:** son la pieza principal de la sección "Tres formas de comer con Carmi": tabla grande 5 / 10 / 20 con precio (de la hoja 2 o del respaldo) y la bebida gratis; "En el local" y "Para llevar y delivery" son líneas simples con link a WhatsApp.
- **Animación (GSAP + ScrollTrigger + Lenis):** hero con entrada en secuencia (titular por palabras con máscara), titulares que suben con máscara, tarjetas del menú en cascada, "tres formas" entrando desde lados distintos, tarjetas de empresas y ubicación que se "destapan" con clip-path, FAQ en cascada, parallax del hero (solo escritorio) y brillo que sigue al mouse en las tarjetas. Solo se animan transform y opacidad, y al terminar se limpian los estilos en línea (`clearProps`) para no pisar el hover de CSS. Las animaciones están en `initAnimations()` y `animateMenuCards()`; si fallan, todo se lleva a su estado final y el contenido nunca queda escondido.
- Se respeta `prefers-reduced-motion` (sin Lenis ni animaciones: `ANIM_OK` queda en falso).
- **SEO:** `lang="es-PY"`, title y description con palabras locales, metas Open Graph y Twitter (sin imagen ni URL hasta tener dominio), JSON-LD de Restaurant + FAQPage con solo datos confirmados (el FAQ es idéntico al visible; si se cambia una respuesta en la sección FAQ, cambiarla también en el JSON-LD), favicon en SVG, `apple-touch-icon.png`, enlace "Saltar al contenido" y respaldo `<noscript>`. Los 10 links de WhatsApp tienen el `href` real escrito en el HTML. Los scripts de GSAP, ScrollTrigger y Lenis van en el `<head>` con `defer` (no bloquean la página). El script de la página corre de inmediato y NO depende de ellos: las animaciones y Lenis arrancan en `startMotion()` (en `DOMContentLoaded`) solo si las librerías llegaron en menos de 2,5 s; si el CDN falla o tarda, el menú, el formulario y WhatsApp funcionan igual, sin animaciones.
- **Accesibilidad y robustez (paso 8):** la guarnición es un `<select>` nativo; las tarjetas del menú solo se ocultan con `opacity` (alcanzables con Tab); menú de secciones con botón en el celular; "Saltar al contenido" mueve el foco; el menú y la hoja 2 se descargan con tiempo máximo de 7 s (`fetchCSV`) y se rechaza cualquier respuesta que sea HTML o tenga filas con menos de 3 columnas; foto que no carga = "Foto próximamente"; precio vacío = "Consultar"; singular "1 vianda"; cantidades repetidas en la hoja 2 se descartan; sin JavaScript se esconden el pizarrón y el formulario y queda un botón de WhatsApp.
- NO hay panel admin, ni localStorage, ni calculadora de viandas. El "panel admin" es la propia hoja de Google Sheets.
- Copia de seguridad del diseño anterior: `LO DE CARMI/landing_v1.html`.

### Pendiente
- Pegar el link CSV de la hoja 2 en `PACKS_CSV_URL`.
- Paso 9: entrega. (Pasos 6, 7 y 8, revisión visual, SEO y QA, ya se hicieron.)
- El menú del Sheets asume que la primera fila es el encabezado (se descarta siempre). Si alguien borra esa fila, se pierde el primer plato.
- Respaldos: `landing_v1.html` (diseño original), `landing_v2_antes-de-seo.html` y `landing_v2_antes-de-qa.html` (se pueden borrar cuando todo esté publicado y probado).
- **Dominio (bloquea la vista previa al compartir):** todavía no hay. Cuando exista (puede ser el `*.vercel.app` al principio), en el `<head>` descomentar el bloque marcado `[COMPLETAR-DOMINIO]` (canonical, og:url, og:image, twitter:image) y reemplazar `https://TU-DOMINIO/` por la dirección real. Subir `og-lo-de-carmi.png` y `apple-touch-icon.png` a la raíz del sitio junto al HTML (renombrado `index.html`). Crear `robots.txt` y `sitemap.xml` con ese dominio. WhatsApp guarda la vista previa en caché: para probar, compartir el link con `?v=2` o usar el Depurador de Facebook.
- Al tener dominio, sumar `url`, `@id` e `image` al JSON-LD. Al tener el número de casa, agregarlo en `streetAddress` del JSON-LD y en el texto de ubicación.
- Respaldo de antes del SEO: `LO DE CARMI/landing_v2_antes-de-seo.html` (se puede borrar cuando todo esté publicado y probado).
- Para probar la página: servirla por http (por ejemplo `npx serve` o subirla a Vercel). Abierta con doble clic (`file://`) el navegador bloquea la lectura del Google Sheets y muestra el aviso de menú caído; en el sitio publicado funciona.
- Ideas de diseño que se dejaron afuera a propósito (se pueden retomar): precios con línea de puntos también en las tarjetas del menú, esquinas menos redondeadas en las tarjetas y un sello rotado tipo "Casero". Hecho en el paso 6: pizarrón en el hero y combos como pieza principal.
- Zona de delivery y número de casa: [COMPLETAR].

## Reglas
1. Nunca inventes datos del negocio (precios, horarios, direcciones, testimonios, cantidad de clientes). Si falta, poné [COMPLETAR].
2. Todavía no hay fotos de platos: usá placeholders claros, no fotos de stock que parezcan reales.
3. Mobile primero: la mayoría entra desde el celular por Instagram o WhatsApp.
4. El objetivo de la página es UNO: que la persona escriba por WhatsApp para pedir o contratar viandas/combos. Todo CTA apunta ahí.
5. Respetar `prefers-reduced-motion`. Las animaciones no pueden tapar el contenido ni trabar el scroll en celulares baratos.
6. Antes de dar algo por terminado: revisar en 375px y 1280px, sin errores en consola, y que el link de WhatsApp abra con el mensaje armado.
7. Hacer cambios en pasadas chicas y guardar una copia antes de un rediseño grande (`landing_vX.html`).
8. Escribir en español de Paraguay, tono cercano y casero, sin sonar a agencia.
