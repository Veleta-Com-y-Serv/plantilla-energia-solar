# Energía solar e instaladores: brief de diseño

Plantilla `energia-solar` creada el 29/10/2026 a partir de `reformas-oficios` con `php artisan plantillas:nueva`
y rediseñada entera (fila 22 del brief de la tanda «a ancho completo»). Este fichero se queda en el repo: es lo
que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: instaladores de placas solares y autoconsumo, baterías, aerotermia, climatización, cargadores de
  coche y electricistas (`sectores`: energia-solar, fotovoltaica, instaladores, climatizacion, aerotermia,
  electricistas). Su cliente es un particular, una empresa con nave o un agricultor que paga mucho de luz: quiere
  saber si le compensa, cuánto cuesta más o menos, qué ayudas hay y si la empresa es seria y de la zona.
- **Qué tiene que conseguir la web**: que pidan el estudio gratis. «Estudio gratis» en la cabecera, el sello del
  hero, el botón principal del hero, soluciones y ayudas llevan al formulario de `presupuesto`; el teléfono está
  en la cabecera (escritorio), preguntas, contacto, pie y barra fija de móvil.
- **Tono y estilo** (`estilo: limpio`): claro, optimista y técnico sin jerga. Referencia que sí: losmartesnohayluna.com
  por las bandas a sangre, la tipografía grande y las bandas de color pleno; la señalética de la energía limpia
  (el sol, la celda fotovoltaica, el horizonte). Que no: la caja centrada estrecha con tarjetas blancas; el
  amarillo obra con Arial Black, mayúsculas y diagonales de `reformas-oficios` (de la que parte); el naranja y
  carbón con franjas de `taller-mecanico`.
- **Paleta de ejemplo**: primario `#0f7a4d` (verde), acento `#ffc83d` (amarillo sol), fondo `#ffffff`, texto
  `#0c1f17` (casi negro verdoso). Derivados en `global.css` con `color-mix`: `--noche` (32 % primario + texto:
  bandas oscuras), `--noche-2` (velos), `--menta` (8 % primario sobre fondo: bandas suaves), `--linea`. La letra
  sobre cada color (`--sobre-primario`, `--sobre-acento`, `--sobre-noche`) se calcula con oklch; cada banda fija
  su color de botón (`--boton`) y de raya (`--raya`), así el diseño aguanta los cuatro colores del cliente.
- **Tipografía**: del sistema. Títulos en "Segoe UI Variable Display" / "SF Pro Display" / system-ui a 800, en
  minúscula, interletrado −0,035 em, interlineado ~1; el del hero llega a 7 rem en escritorio (2,75 en móvil).
  Antetítulos de 0,78 rem en mayúsculas espaciadas (0,18 em) con una raya de color delante. Texto en system-ui.
- **Formas**: botones píldora; el sol (disco amarillo con dos halos translúcidos) en el sello del hero, los iconos
  de ventajas, presupuesto y contacto, el marcador de zonas, la marca y el «+» abierto de las preguntas; el
  horizonte: borde inferior curvo del hero (`clip-path: ellipse`) y borde superior curvo del pie (SVG); la celda
  fotovoltaica: rejilla fina de 72×44 px sobre las bandas oscuras (`.celdas`) y el panel de soluciones con filetes.
- **Ritmo de bandas** (todas de borde a borde; contenido hasta 90 rem, 16 px de margen en móvil):
  1. `hero` — foto a sangre 92 svh con velo verde noche desde la izquierda, título enorme, dos botones, sello del
     sol a la derecha (en móvil, sello redondeado) y garantías en fila; borde inferior curvo.
  2. `ventajas` — blanco; titular partido; cuatro columnas con filetes y un sol con icono.
  3. `soluciones` — verde noche con celdas; panel de 4×2 celdas (2 en tableta, 1 en móvil con el icono junto al
     título) con precio «desde» en píldora amarilla, opcional.
  4. `proceso` — amarillo sol con un gran disco claro en la esquina; pasos en línea con discos verde noche.
  5. `subvenciones` — partida: foto a sangre a la izquierda, menta a la derecha con lista de ayudas y aviso.
  6. `zonas` — partida al revés (zigzag): texto con píldoras de pueblos a la izquierda, foto con marcador a la derecha.
  7. `cifras` — verde con cuatro números enormes entre filetes y un sol que asoma por la esquina (escritorio).
  8. `trabajos` — titular en blanco y mosaico de fotos de borde a borde sin márgenes (2×2 + cuatro + franja).
  9. `opiniones` — menta; titular centrado; tres columnas con filetes, comilla en un sol.
  10. `preguntas` — blanco; titular fijo con el teléfono a la izquierda, acordeón con filetes a la derecha.
  11. `presupuesto` — partida en dos colores a sangre: verde noche con garantías y amarillo sol con el formulario.
  12. `contacto` — partida: teléfono enorme y datos a la izquierda, foto de la nave a sangre a la derecha.
  Pie: verde noche con celdas, horizonte curvo arriba y cuatro columnas (marca y teléfono, contacto, web, zonas).
  Cabecera fija: transparente sobre la foto del hero y blanca al bajar (o al abrir el menú). Barra fija de móvil:
  «Llamar» amarillo y «WhatsApp» con borde, en píldoras sobre verde noche.
- **Apartados y listas propias**: `soluciones.soluciones` (`titulo, texto, icono, precio`), `trabajos.trabajos`
  (`titulo, lugar, potencia, texto, imagen`, `imagen_antes` opcional), `subvenciones.items` (`titulo, texto`) +
  `nota`, `hero.items` (`titulo, icono`). Las que salen vacías no se pintan (cifras, preguntas) o pintan solo su
  titular (soluciones, trabajos, opiniones).
- **Fotos** (`fotos.json`, 10): tejado con placas en la llanura de Lleida (hero, 21:9), adosado con placas
  (ayudas), vista aérea del Segrià (zonas), seis trabajos (vivienda, nave de fruta, bombeo para riego, granja,
  aerotermia en patio, pérgola con cargador) y la nave del instalador (contacto). Sin texto legible, sin logotipos,
  sin matrículas ni personas. De respaldo, `public/placeholders/` (hero, tejado, campo, nave, mapa, persona).
- **Qué no hacer**: tarjetas blancas flotando en una caja estrecha; mayúsculas pesadas y diagonales (son de
  `reformas-oficios`); porcentajes o importes de ayudas en los componentes (las ayudas cambian: van en
  `site.yaml` y sin cifras inventadas); precios o cifras fijos en los componentes; fotos de personas.

## Páginas propias (fichas y zonas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista; en las zonas, entrada, texto de la zona, servicios, trabajos del lugar, opiniones y contacto.
