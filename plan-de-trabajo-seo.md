# Plan de trabajo SEO · Robotines

Basado en la auditoría de INFOSAMA del 5 de octubre de 2026 (nota 58/100). Plataforma: PrestaShop.

Cómo usarlo: cada tarea tiene **pasos**, **criterio de hecho** (cuándo se da por cerrada) y la **métrica** que debe moverse. El orden respeta dependencias: no se optimiza nada hasta saber si la caída es real y hasta medir bien.

---

## Resumen del calendario

| Fase | Plazo | Tareas | Resultado esperado |
|---|---|---|---|
| 0 · Diagnóstico | Semana 1 | T1–T3 | Saber si hay pérdida real y medir ventas reales |
| 1 · Limpieza y mejoras rápidas | Semanas 2–5 | T4–T13 | Más clics sin subir posiciones; web sin errores |
| 2 · Velocidad y contenido | Meses 2–3 | T14–T20 | Web rápida y posiciones en búsquedas de volumen |
| 3 · Autoridad | Continuo | T21–T23 | Menos dependencia de la marca |

---

## Fase 0 · Semana 1 — Diagnóstico

### T1 · Confirmar la caída del 30 de septiembre (crítico)
Las palabras Gundam pasaron del puesto 1 a fuera del top 100 en el seguimiento; Search Console aún no tenía datos de esas fechas.

1. Search Console › Rendimiento: comparar 7 días antes del 30/09 con 7 días después. Filtrar consultas que contengan «gundam» y la URL de la categoría Gundam.
2. Comprobar a mano en incógnito (o con la herramienta de seguimiento, ubicación España, móvil) «gundam maquetas», «maquetas gundam», «gundam mega».
3. Inspección de URL de la categoría Gundam: indexada, canonical declarado = canonical elegido por Google, sin noindex, robots.txt sin cambios.
4. Revisar qué cambió en la web entre el 25/09 y el 30/09: módulos actualizados, cambio de URL de categoría, robots.txt, plantilla, servidor.
5. Consultar el panel de estado de Google Search por si hubo actualización del algoritmo esas fechas.
6. Decisión:
   - Clics e impresiones en GSC estables → fallo del seguimiento; documentarlo y cerrar.
   - Caída real con causa técnica → corregir y pedir reindexación.
   - Caída real sin causa técnica → seguir semanalmente y priorizar T7, T15 y T21.

**Hecho cuando:** hay una conclusión escrita (real / no real + causa).
**Métrica:** clics semanales de consultas Gundam.

### T2 · Arreglar la medición de Analytics (alto)
GSC: ~3.300 clics/mes. GA4: 689 visitas y 13 compras. La diferencia es demasiado grande.

1. Con Tag Assistant, abrir portada, categoría, ficha, carrito y confirmación de pedido: comprobar que la etiqueta GA4 se dispara y con qué ID de medición.
2. Revisar el módulo de GA4/GTM de PrestaShop tras la migración: ID correcto, una sola etiqueta (sin duplicados ni propiedad antigua).
3. Revisar el banner de cookies: modo de consentimiento v2 activo; GA4 debe cargarse en modo básico/avanzado aunque se rechacen cookies, no bloquearse entero.
4. Verificar el evento `purchase` con un pedido de prueba (valor, moneda, ID de transacción).
5. Cruzar pedidos de septiembre del back office con compras de GA4.
6. Excluir tráfico interno y comprobar que no hay filtros que eliminen visitas.

**Hecho cuando:** compras GA4 ≈ pedidos reales (±10 %) y sesiones orgánicas GA4 razonablemente cercanas a los clics de GSC (la diferencia restante se explica por el consentimiento).
**Métrica:** sesiones orgánicas, compras e ingresos orgánicos en GA4.

### T3 · Foto de partida
1. Exportar de GSC los últimos 16 meses: consultas, páginas, clics, impresiones, CTR, posición.
2. Guardar títulos, descripciones, canonicals y H1 de las 50 páginas con más impresiones.
3. Anotar en GA4/GSC las fechas de cada cambio de este plan.

**Hecho cuando:** existe una hoja con los datos base para comparar cada mes.

---

## Fase 1 · Semanas 2–5 — Limpieza y mejoras rápidas

### T4 · Corregir los 90 errores 404 enlazados desde la web (alto)
Ya localizados 46 enlaces rotos en 26 páginas (rastreo del 7/10):

| Página que enlaza | Enlace roto | Acción |
|---|---|---|
| Portada `/es/` | `/es/1826-master-grade-ex` | Cambiar por la categoría vigente |
| Marca Mr. Hobby | `/es/34-mr-hobby`, `/es/136-acrilicas`, `/es/1542-mr-color-spray` | Cambiar por las URL actuales |
| Perfect Grade | `/es/7-real-grade` | Cambiar por `/es/81-real-grade` |
| Pinturas y complementos | `/es/923-tamiya` | Cambiar por la marca Tamiya actual |
| Batman | `/es/25-pinzas`, `/es/606-vengadores` | Actualizar o quitar |
| Evangelion | `/es/134-digimon`, `/es/166-macross-frontier`, `/es/468-full-metal-panic` | Actualizar o quitar |
| Tanques | `/es/672-vitrinas` | Actualizar o quitar |
| Maquetas Mazinger Z | `/es/maquetas-anime` | Actualizar o quitar |
| SD Gundam, merchandising, gashapones, videojuegos | `/es/1893-maquetas-series` | Actualizar o quitar |

1. Editar los textos de esas categorías/marcas en el back office (Catálogo › Categorías › Descripción) y el módulo de la portada.
2. Crear 301 de cada URL antigua a su equivalente actual (módulo de redirecciones o `.htaccess`), para recuperar enlaces externos y marcadores.
3. Rastrear la web completa (Screaming Frog o similar, excluyendo parámetros de filtros) para localizar los ~50 404 restantes y repetir 1–2.
4. Revisar en GSC › Páginas › «No encontrado (404)».

**Hecho cuando:** un rastreo completo no devuelve enlaces internos a 404.

### T5 · Enlaces del Aviso legal (medio)
1. Cambiar los enlaces a Política de privacidad y Cookies (hoy llevan a «Reservas» y «Sugerencias») por las URL correctas.
2. Revisar los mismos enlaces en el pie de página y en el banner de cookies.

**Hecho cuando:** ambos enlaces abren la página correcta en es, en y fr.

### T6 · Reducir las 325 redirecciones internas (medio)
1. Del rastreo de T4, exportar los enlaces internos que apuntan a una URL con 301 (137 categorías, 91 filtros, 91 fichas).
2. Ordenar por número de enlaces entrantes y corregir primero menú, pie y portada.
3. Cambiar cada enlace por la URL final; mantener las 301 activas.

**Hecho cuando:** menú, pie, portada y categorías principales no enlazan a ninguna 301.

### T7 · Títulos y descripciones de páginas con muchas apariciones (alto · mayor impacto rápido)
Objetivo: subir el CTR del 2 % al 3 % (≈ +1.500 clics/mes estimados).

1. Empezar por estas páginas (propuestas de la IA como punto de partida, revisar una a una):

| Página | Apariciones | CTR | Título propuesto (revisar) |
|---|---|---|---|
| `/en/169-mak` | 2.145 | 2,0 % | Ma.K Model Kits … – Robotines (en inglés, no mezclar idiomas) |
| `/es/268-one-piece` | 863 | 1,3 % | One Piece Maquetas: Barcos, Figuras y Ediciones Limitadas \| Robotines |
| `/es/contactenos` | 827 | 0,5 % | Revisar qué consultas la muestran |
| `/es/1395-dinosaurios-para-principiantes` | 818 | 0,5 % | Maquetas de Dinosaurios para Principiantes – Bandai, Tamiya \| Robotines |
| `/es/277_modelcraft` | 778 | 0,3 % | Comprar Herramientas Modelcraft \| Catálogo y Precios – Robotines |
| `/es/1896-outlet` | 752 | 0,5 % | Outlet Maquetas y Herramientas \| Ofertas Modelismo – Robotines |
| Ficha AK Interactive Playmarkers | 636 | 1,1 % | Redactar |
| `/es/399-cabinas` | 635 | 1,9 % | Redactar |
| Ficha Pintura Acrílica Tamiya X y XF | 564 | 1,4 % | Pintura Acrílica Tamiya X y XF – Gama Completa \| Robotines |

2. Ampliar a las 50 páginas con más impresiones y CTR < 2 % (export de GSC de T3).
3. Reglas de redacción: palabra clave al inicio, ≤ 60 caracteres, beneficio (envío gratis desde 99 €, 4,9/5, stock), sin emojis en el título.
4. Descripciones vacías (358 fichas y 141 categorías): plantilla por tipo con carga masiva CSV, p. ej. *«{Producto} de {Marca} en stock. Envío gratis desde 99 € y 4,9/5 en +5.000 opiniones. Compra en Robotines.»* Luego personalizar a mano las de más impresiones.
5. No tocar el título de la portada (ya está trabajado).

**Hecho cuando:** las 50 páginas revisadas y 0 fichas/categorías indexables sin descripción.
**Métrica:** CTR por página a las 4 semanas frente a T3.

### T8 · Sacar de Google las páginas de acceso (alto)
Las URL `autenticación?back=…` salen en Google para productos. El robots.txt las bloquea, por eso Google no puede leer un noindex.

1. Añadir `<meta name="robots" content="noindex, nofollow">` en la plantilla de autenticación/inicio de sesión.
2. Quitar temporalmente el bloqueo de esas URL en robots.txt para que Google vea el noindex.
3. Añadir `rel="nofollow"` a los enlaces de «Iniciar sesión para comprar/valorar» que generan esas URL.
4. GSC › Retiradas: solicitar retirada temporal por prefijo.
5. Cuando desaparezcan del índice (GSC › Páginas), decidir si se vuelve a bloquear en robots.txt (mejor dejar solo el noindex).

**Hecho cuando:** `site:robotines.com inurl:autenticacion` no devuelve resultados.

### T9 · Mapa del sitio actualizado (alto)
1. Configurar el módulo de sitemap (p. ej. gsitemap) con una tarea cron diaria.
2. Comprobar que `lastmod` refleja la fecha real de modificación.
3. Excluir del sitemap URL con noindex, redirecciones, 404, filtros y variantes de color.
4. Reenviar en GSC y revisar que «Descubiertas» ≈ «Indexadas» por tipo de página.

**Hecho cuando:** fechas actuales y 0 URL no indexables en el sitemap.

### T10 · Página «Envíos gratuitos» indexable (medio)
1. Quitar el noindex.
2. Ampliar de 38 a ~300 palabras: umbral, plazos, zonas, transportistas, preguntas frecuentes.
3. Escribir título y meta description; enlazar desde el pie y el carrito.
4. Revisar también Devoluciones (26 apariciones): meta description y FAQ.

### T11 · Versión francesa en hreflang (medio)
1. Añadir `hreflang="fr"` en todas las páginas junto a es, en y `x-default`.
2. Validar reciprocidad (cada idioma enlaza a los demás) con un rastreo.

### T12 · Datos estructurados y redes (medio)
1. Añadir `shippingDetails` y `hasMerchantReturnPolicy` en `Offer` (o la política de devoluciones a nivel `Organization`).
2. Eliminar el bloque duplicado de opiniones y corregir los que tienen autor vacío.
3. Añadir etiquetas `twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`.
4. Validar con la prueba de resultados enriquecidos y revisar GSC › Fragmentos de producto / Fichas de comerciante.

### T13 · Detalles on-page (bajo)
1. H1 en la portada `/en/`.
2. Título en las 4 categorías del blog en inglés.
3. Texto alternativo en las 22 imágenes de la portada que lo tienen vacío.
4. Decidir política de emojis: fuera de títulos; en H1 opcional (162 páginas).
5. Listados paginados: mantener canonical propio en cada página (no a la página 1, como propone la IA), título con «– Página 2» en vez de «(2)» y sin repetir la descripción de la categoría.

---

## Fase 2 · Meses 2–3 — Velocidad y contenido

### T14 · Velocidad (crítico)
Situación: HTML de 0,5 MB en portada y 1,3 MB en fichas, 4.640 elementos, 115 imágenes, 957 enlaces en portada, ~10 s de carga completa.

1. Medir punto de partida: PageSpeed Insights (datos de campo CrUX) en portada, categoría y ficha; anotar LCP, INP y CLS.
2. Menú: reducir el megamenú (es la causa principal de los 957 enlaces y miles de elementos). Dejar categorías de primer y segundo nivel; el resto, en páginas de categoría. Alternativa: cargarlo bajo demanda.
3. Fichas de 1,3 MB: identificar qué ocupa el HTML (combinaciones/colores en JSON, opiniones, productos relacionados, módulos) y paginar o cargar en diferido.
4. Imágenes: `loading="lazy"` bajo el primer pantallazo, WebP, tamaños `width`/`height` declarados, imagen principal con `fetchpriority="high"`.
5. Módulos: desactivar los que no se usen; CCC de PrestaShop (combinar, comprimir y caché de CSS/JS); diferir JS no crítico.
6. Repetir mediciones tras cada cambio.

**Objetivos:** < 1.500 elementos en portada, HTML < 200 KB, LCP < 2,5 s, INP < 200 ms, CLS < 0,1 en móvil.
**Límite:** depende del tema; si no se alcanza, valorar cambio de tema.

### T15 · Páginas que compiten entre sí (medio)
| Conflicto | Acción |
|---|---|
| Ma.K español vs inglés | Revisar hreflang y que cada versión esté en su idioma |
| «gunpla» / «gundam» entre portada y categorías | Elegir una URL por consulta; ajustar títulos y anclas internas hacia ella |
| «modelismo militar» maquetas vs figuras | Diferenciar títulos; enlazar entre ambas |
| Sets de color Vallejo | Diferenciar títulos y descripciones o consolidar |

**Hecho cuando:** en GSC cada consulta muestra una sola URL dominante.

### T16 · Control de filtros y paginación (medio)
120 URL con `?page=` o filtros concentran el 25 % de las apariciones.

1. Identificar en GSC qué combinaciones de filtro tienen impresiones y clics.
2. Las útiles (p. ej. marca dentro de categoría con búsquedas propias): convertirlas en subcategorías o landings con URL limpia.
3. El resto: noindex y no incluir en el sitemap; evitar enlazarlas desde el menú.
4. Revisar que las variantes de color (136 páginas auditadas) siguen canonizadas y fuera del sitemap.

### T17 · Recuperar «super deformed» y SD Gundam (alto · 14.800 búsquedas/mes)
La categoría llegó a estar en el puesto 3 y hoy no sale en el top 100.

1. Analizar la SERP de «super deformed» y «sd gundam»: ¿Google muestra tiendas o resultados informativos? Si no muestra tiendas, apuntar a variantes comerciales («maquetas sd gundam», «sd gundam ex standard», «sdcs»).
2. Comprobar si la URL de la categoría cambió (301), está indexada y es la canónica.
3. Reforzar la categoría: texto de 300–500 palabras (qué es SD, gamas SD EX-Standard, SDCS, BB Senshi, dificultad, herramientas), FAQ, título y H1 con «SD Gundam / Super Deformed».
4. Enlazar desde la categoría Gundam, el menú y la guía de T20.
5. Corregir el enlace roto que tiene (`/es/1893-maquetas-series`).

### T18 · Palabras a un paso de la primera página (alto · ~1.900 búsquedas/mes)
«modelismo maquetas», «tienda maquetas», «modelismo tiendas» (puestos 17–18), además de «modelistas» (17) y «modelismo» (28).

1. Ver en GSC qué URL posiciona para cada una.
2. Si es la portada: incluir los términos en título/H1/texto de forma natural y añadir un bloque de texto (quiénes sois, catálogo, marcas oficiales, envío).
3. Añadir enlaces internos con esas anclas desde blog y categorías.
4. Combinar con T21 (enlaces externos) para ganar autoridad.

### T19 · Barcos y trenes frente a la competencia (medio)
«maquetas de barcos» (1.600, puesto 44), «maquetas de trenes venta» (puesto 25).

1. Revisar las categorías frente a El Taller del Modelista: texto, filtros útiles, marcas, guía de escalas.
2. Ampliar texto, FAQ y enlaces internos; título orientado a compra.

### T20 · Tres guías de blog (medio)
1. «Cómo pintar maquetas Gundam para principiantes» → enlaza a pinturas, marcadores, herramientas.
2. «Mejores herramientas y pinceles de precisión» → Mr. Hobby, Modelcraft, Tamiya.
3. «Maquetas Pokémon: Bandai frente a Takara Tomy» → ayuda a decidir.

Para cada guía: brief con palabra clave, intención y estructura; 1.500–2.500 palabras; fotos propias; autor identificado (experiencia); enlaces a 5–10 productos/categorías; schema `Article`; enlace desde categorías relacionadas.

---

## Fase 3 · Continuo — Autoridad y seguimiento

### T21 · Enlaces externos de calidad (alto)
133 dominios, 86 % basura (generados por terceros).

1. Basura: no desautorizar en bloque; Google los ignora. Solo actuar si aparece una acción manual en GSC.
2. Fabricantes y distribuidores (DXM Decals, Mr. Hobby Europe, VMS, Zoukei-Mura, Bandai, Tamiya, Kotobukiya, Kagero): pedir aparecer en su listado de distribuidores oficiales.
3. Clubes y asociaciones de modelismo: patrocinio de concursos y exposiciones a cambio de mención con enlace.
4. Foros, blogs y canales de YouTube de modelismo: envío de kits para reseñas.
5. Medios y prensa local: historia de la tienda (desde 2011, 4,9/5).
6. Las guías de T20 como contenido enlazable.

**Objetivo:** 2–4 dominios reales nuevos al mes.

### T22 · Seguimiento de posiciones y de IA (bajo)
1. Ampliar las 56 palabras seguidas con las de T17–T19.
2. Configurar 10–20 preguntas en asistentes de IA (ChatGPT, Gemini, Perplexity), p. ej. «mejor tienda de maquetas Gundam en España», y revisar menciones cada mes.
3. Mantener `llms.txt` actualizado.

### T23 · Informe mensual
| KPI | Fuente | Hoy | Objetivo a 3 meses |
|---|---|---|---|
| Clics orgánicos/mes | GSC | ~3.300 | 4.500 |
| % clics sin marca | GSC | 46 % | 55 % |
| CTR medio | GSC | ~2 % | 3 % |
| Palabras en primera página | Seguimiento | 11 | 25 |
| Compras orgánicas | GA4 | 13 (infravalorado) | Medición correcta, luego crecer |
| Errores 404 internos | Rastreo | 90 | 0 |
| LCP móvil | CrUX | por medir | < 2,5 s |
| Dominios de calidad que enlazan | Herramienta de enlaces | ~19 | 30 |

Los objetivos son estimaciones; ajustarlos tras T1 y T2.

---

## Viabilidad en PrestaShop

| Tarea | Viable | Cómo |
|---|---|---|
| Títulos y descripciones | Sí | Panel o CSV |
| Envíos/devoluciones en schema, tarjetas X | Sí | Pequeño cambio de plantilla |
| Sitemap actualizado | Sí | Tarea cron |
| Páginas de acceso fuera de Google | Sí | noindex en plantilla |
| Guías | Sí | Módulo de blog instalado |
| Menú y velocidad | Parcial | Depende del tema |
| Fichas de color con URL propia | Limitado | Solo canonical |
| Filtros por facetas | Limitado | Control continuo |

## Advertencias del propio informe
- Se descartan las 913 recomendaciones de enlazado interno de la herramienta de IA (dato no calculado; la portada tiene 957 enlaces).
- La auditoría IA solo cubrió 1.000 de ~32.000 páginas por idioma.
- Las cifras de competencia y la previsión de +1.500 clics son estimaciones.
