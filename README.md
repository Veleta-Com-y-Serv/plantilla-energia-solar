# Plantilla NoExpertise · Energía solar e instaladores

Web limpia a todo el ancho para instaladores solares: soluciones, ayudas, trabajos y estudio gratis.

- Sectores: energía solar, fotovoltaica, instaladores, climatización, aerotermia, electricistas. Estilo: limpio. Plan mínimo: gratis.
- Secciones: hero, ventajas, soluciones, proceso, subvenciones, zonas, cifras, trabajos, opiniones, preguntas, presupuesto, contacto (+ `texto` para apartados nuevos).
- Campos propios: `hero.destacado` (sello del sol) y `hero.items` (garantías), `soluciones.soluciones[]` (`titulo, texto, icono, precio` opcional), `subvenciones.items[]` + `subvenciones.nota`, `trabajos.trabajos[]` (`titulo, lugar, potencia, texto, imagen`, `imagen_antes` opcional), `presupuesto.nota` y `presupuesto.boton_formulario`, `cifras.items` (no se pinta vacía).
- Ejemplo: Solana Ponent, instaladores de placas solares, baterías y aerotermia en Lleida y el Segrià (negocio ficticio).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (con `areaServed` desde `zonas`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.
