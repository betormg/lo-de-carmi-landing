---
name: mejorar-landing
description: Ruta completa para mejorar la landing de Lo de Carmi paso a paso (copy, diseño, animación, revisión, SEO, QA). Se usa con /mejorar-landing.
disable-model-invocation: true
---
Vamos a mejorar la landing siguiendo esta ruta. Hacé UN paso por vez, mostrame el resultado y esperá mi OK antes del siguiente. Paso pedido (si está vacío, empezá por el 1): $ARGUMENTS

1. **Diagnóstico**: leé CLAUDE.md y el HTML. Decime en una lista corta qué está bien, qué falta para vender y qué está roto. No edites nada.
2. **Copy**: usá el subagente copywriter (y la skill copywriting/page-cro si está instalada) para reescribir hero, viandas, combos prepagos, ubicación, FAQ y footer. Renombrar "Tres formas de disfrutar". Mostrame el texto antes de aplicarlo.
3. **Dirección visual**: con la skill frontend-design, proponé 2 direcciones con fondo oscuro (paleta, tipografías, estilo de tarjetas). Podés inspirarte en `_estilos-design-md/` sin copiar marcas. Esperá que elija una.
4. **Construcción**: guardá una copia `landing_vX.html` y aplicá copy + diseño. No toques la lógica de Google Sheets, calculadora ni WhatsApp salvo que esté rota.
5. **Animación**: con gsap-skills y Context7, sumá Lenis + ScrollTrigger: un hero con entrada fuerte, revelado de secciones con variedad (no fade-up en todo), hover en tarjetas. Respetar prefers-reduced-motion.
6. **Revisión visual**: corré el subagente ui-reviewer y arreglá lo Crítico e Importante.
7. **SEO y velocidad**: corré seo-auditor y aplicá meta, Open Graph y JSON-LD.
8. **QA**: corré qa-tester y arreglá todo lo que falle.
9. **Entrega**: resumen de cambios, lista de [COMPLETAR] pendientes y qué falta para publicar.
