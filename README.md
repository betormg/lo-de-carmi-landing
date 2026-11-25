# Lo de Carmi · Web

Landing de **Lo de Carmi Resto Bar** (comida casera y viandas, Asunción, Paraguay).
Su objetivo es uno: que la gente escriba por WhatsApp para pedir.

**Sitio publicado:** https://lo-de-carmi.vercel.app

El menú del día sale de la base de datos del
[sistema de caja](https://github.com/betormg/Ticket-System-Lo-de-Carmi-Resto-Bar).

## Qué tiene

- Menú del día con selector de guarnición por plato
- Combos prepagos de viandas
- Formulario que arma el mensaje y abre WhatsApp (vianda, combo o corporativo)
- Información para empresas, preguntas frecuentes y ubicación
- Metadatos para buscadores y para compartir, y respeto por "reducir movimiento"

## Tecnologías

Un solo archivo HTML con CSS y JavaScript, sin framework ni paso de build.
GSAP, ScrollTrigger y Lenis (por CDN) para las animaciones y el scroll.

## De dónde salen los datos

1. **Menú:** la función pública `web_menu_hoy()` de Supabase devuelve los platos con
   stock cargado hoy y las guarniciones del día. Los agotados no se muestran.
2. **Respaldo:** si no hay stock cargado o la base no responde, se lee una hoja de
   Google Sheets publicada como CSV.
3. **Combos:** precios definidos en la página, con opción de leerlos de una hoja de
   cálculo.

La clave de Supabase que aparece en el código es la *publishable*, pensada para usarse
en el navegador. El acceso a los datos lo controla Row Level Security en la base.

## Verlo en la computadora

Hay que servir la carpeta `publicar/` por HTTP (abrir el archivo con doble clic bloquea
la lectura de la hoja de cálculo):

```bash
npx serve publicar
```

## Publicar

Desde la carpeta `publicar/`:

```bash
vercel deploy --prod
```

## Autor

Roberto Mendoza · [github.com/betormg](https://github.com/betormg)
