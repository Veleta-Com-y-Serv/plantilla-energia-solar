# Plantilla «Energía solar e instaladores» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **limpio**
(verde + amarillo sol + blanco, bandas a todo el ancho, titulares en sans de sistema muy pesada y en minúscula,
botones píldora, el sol como disco amarillo con halos, horizonte curvo en la portada y el pie, rejilla de celda
fotovoltaica en las bandas oscuras). Todo en castellano de España, frases cortas, sin jerga. El brief de diseño
completo está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` deriva el resto con `color-mix`:
  - `primario` = verde: botones en bandas claras, banda de cifras, marcas de verificación, teléfono grande.
  - `acento` = amarillo sol: botones en bandas oscuras, banda de proceso, sellos, iconos en disco, formulario de presupuesto.
  - `--noche` (primario + texto): bandas oscuras (soluciones, presupuesto, pie, portada sin foto). `--menta` (primario muy claro): ayudas, opiniones.
  - La letra encima de cada color se calcula sola (`--sobre-primario`, `--sobre-acento`, `--sobre-noche`: negra si el color es claro, blanca si es oscuro).
- **Tipografías y aspecto general**: `src/styles/global.css` (pilas del sistema: `--fuente-titulos` = "Segoe UI Variable Display", "SF Pro Display", system-ui… a 800; bandas `.banda-clara/.banda-menta/.banda-noche/.banda-verde/.banda-sol`, `.celdas`, `.antetitulo` con raya, `.titular-partido`, `.btn`/`.btn-sec` píldora, `.disco`, filas partidas a sangre `.partida`/`.partida-foto`/`.partida-texto`, cabecera `.cabecera-solar`, pie `.pie-solar` y barra fija de móvil). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un sol amarillo + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho y pintan bien con listas y campos vacíos.
- `hero` → `hero.astro`: foto a sangre (92 svh) con velo verde noche, título enorme, `texto`, `cta` y `cta_secundario`; `destacado: {titulo, texto}` en un sol amarillo («Estudio gratis en 48 h»); `items: [{titulo, icono}]` como garantías en fila. Borde inferior curvo. La cabecera va transparente encima.
- `ventajas` → `ventajas.astro`: titular partido y `items: [{titulo, texto, icono}]` en columnas con filetes (4/2/1). `cta` opcional.
- `soluciones` → `soluciones.astro`: banda verde noche con celdas; `soluciones: [{titulo, texto, icono, precio}]` como panel de celdas (4/2/1). `precio` opcional («desde 4.900 €», «Consultar» o vacío: no se pinta). Sus títulos son las opciones de «¿Qué te interesa?» del formulario de presupuesto. `cta` junto al titular.
- `proceso` → `proceso.astro`: banda amarilla sol; `items: [{titulo, texto, icono}]` en línea horizontal (vertical en móvil) con discos numerados.
- `subvenciones` → `subvenciones.astro`: fila partida con `imagen` a sangre a la izquierda y banda menta; `items: [{titulo, texto}]` con marcas, `nota` (aviso de que las ayudas cambian) y `cta`. **No pongas porcentajes ni importes de ayudas** que no dé el cliente.
- `zonas` → `zonas.astro`: fila partida con `imagen` a sangre a la derecha; `texto` (radio de trabajo), `items: [{titulo: localidad}]` como píldoras, `cta` opcional. Las primeras 8 localidades salen también en el pie.
- `cifras` → `cifras.astro`: banda verde con `items: [{titulo: "+450", texto}]` enormes. **No se pinta si `items` está vacío.** No inventes cifras.
- `trabajos` → `trabajos.astro`: titular y mosaico de borde a borde; `trabajos: [{titulo, lugar, potencia, texto, imagen}]` (`potencia` opcional, «6,5 kWp»; `imagen_antes` opcional: miniatura «Antes», texto en `etiqueta_antes`). En escritorio el 1.º de cada seis ocupa 2×2 y el 6.º una franja ancha.
- `opiniones` → `opiniones.astro`: banda menta; `testimonios: [{texto, autor, nota}]` en columnas con filetes. No inventes opiniones.
- `preguntas` → `preguntas.astro`: titular fijo a la izquierda con el teléfono y acordeón `details/summary` a la derecha. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: fila partida en dos colores: verde noche con titular, `items` (garantías con icono) y `nota`; amarillo sol con el formulario completo (nombre, teléfono, localidad, «¿Qué te interesa?», gasto de luz, mensaje). `boton_formulario` opcional.
- `contacto` → `contacto.astro`: fila partida: titular, teléfono enorme y datos de `contacto` a la izquierda; `imagen` a sangre a la derecha. Si `presupuesto` no está activa, a la derecha va el formulario de contacto.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` a sangre a la derecha, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura alternar bandas oscuras y claras (soluciones, presupuesto y cifras son oscuras; proceso es amarilla) y no poner seguidas dos filas partidas con la foto del mismo lado.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios, potencias y cifras siempre como texto entre comillas (`"desde 4.900 €"`, `"6,5 kWp"`, `"+450"`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`. En páginas que no son la portada la cabecera es sólida y deja su hueco sola.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: soluciones`, `tipo: trabajos`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y `Titular`, como una banda a todo el ancho (`seccion banda-…` + `contenedor`, o `partida`). `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera), 16 px de margen lateral del texto en móvil (`.contenedor`, `.partida-texto`) con las fotos y fondos tocando el borde, sin scroll horizontal, botones de 44 px o más, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (del sector: `panel, bateria, sol, rayo, ventilador, copo, coche, fabrica, gota, termometro, enchufe, hoja, documento, grafico, euro, herramienta, escudo, casa`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento y páginas por zona)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.soluciones.soluciones` → `/soluciones/<slug>/` (solución).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Zonas: cada elemento de `secciones.zonas.items` **con `texto`** (60-150 palabras: qué trabajos se hacen allí, pueblos cercanos)
  tiene su página en `/zonas/<slug>/`. En la sección: `titulo_pagina` («Reformas en {zona}») y `texto_pagina` (entrada, con {zona} y {negocio}).
- Una orden «añade una página para X» = escribir su `detalle` (o el `texto` de la zona) en site.yaml. Nunca crees a mano páginas en
  `src/pages/soluciones/` ni en `src/pages/zonas/`: salen solas de `src/pages/[coleccion]/[slug].astro` y `src/pages/zonas/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay; zonas con `areaServed`).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
