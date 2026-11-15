# ESTADO — Central Culinaria (demo de la web B2B)

_Resumen operativo a 15/11/2026. Solo hitos: lo que está en curso vive en los PRs. Tope de 100 líneas; lo viejo pasa entero a `docs/historico/ESTADO-AAAA-MM.md` y se enlaza desde aquí._

**Aviso:** este repo guarda solo la web ya compilada. La fuente no está aquí (ver «Bloqueos»).

## Objetivo

Tener publicada una demo (prototipo) de la web B2B de Central Culinaria, cerrada a buscadores.

El paso siguiente con el cliente (web definitiva, dominio, fechas): no consta.

## Hito en curso

- **Hecho:** demo publicada en GitHub Pages. Dos commits, los dos del 18/09/2026. Sin cambios desde entonces.
- **En curso hoy (15/11/2026):** mini cerebro del repo (`AGENTS.md`, `CLAUDE.md`, `ESTADO.md`). Solo documentación.
- Otro hito abierto: no consta.

## Decisiones

Las de 2026-09-18 llevan la fecha de los dos commits. Cuándo y quién decidió cada una: no consta.

- 2026-09-18 — La demo se publica en GitHub Pages desde `main` (raíz), bajo la ruta `/central-culinaria-demo/`. Por qué: no consta.
- 2026-09-18 — Cerrada a buscadores: `noindex, nofollow` en las 35 páginas y `Disallow: /` en `robots.txt`. La descripción del repo dice «prototipo, noindex».
- 2026-09-18 — Canónicos, `sitemap.xml` y datos estructurados apuntan a `www.centralculinaria.com`, no a la URL de la demo. Si el dominio está confirmado con el cliente: no consta.
- Fecha no consta — El repo guarda solo lo compilado; la fuente queda fuera (ficha de Lince, actualizada el 20/10/2026).
- Fecha no consta — Sin modelos de IA ni APIs (ficha de Lince; comprobado hoy en `assets/js/`).
- 2026-11-15 — Se monta el mini cerebro y se conecta a Lince (bloque «Cerebro general» de `AGENTS.md`).
- 2026-11-15 — El repo se conserva (así viene en el encargo del mini cerebro).

## Rama y PR en curso

- Rama `claude/mini-cerebro`, con el PR #1 contra `main`: «Mini cerebro: AGENTS, CLAUDE y ESTADO con tope». Toca solo `AGENTS.md`, `CLAUDE.md` y `ESTADO.md`.
- Antes de este PR solo existía `main`, sin ningún PR abierto ni cerrado (mirado el 15/11/2026).
- Nada movido a `docs/historico/`: no había ficheros previos.

## Pruebas

No hay pruebas ni órdenes de prueba en el repo (no hay `package.json` ni README).

Para el PR del mini cerebro **no se ha compilado nada, ni servido la web en local, ni abierto en un navegador**. Solo lectura de ficheros y dos peticiones con `curl`, el 15/11/2026:

- `git ls-files '*.html' | wc -l` → 35.
- `grep -l noindex $(git ls-files '*.html') | wc -l` → 35.
- `grep -c '<loc>' sitemap.xml` → 33. Quedan fuera `404.html` y `blog/index.html`.
- `grep -rE 'fetch\(|XMLHttpRequest|sendBeacon|WebSocket' assets/js` → sin resultados.
- `assets/js/chunks/form-WFGZRJDY.js`: el envío hace `preventDefault()` y enseña el mensaje de «enviado». No manda datos.
- `grep -l 'class="proto-note' $(git ls-files '*.html') | wc -l` → 27 páginas con nota de «Prototipo»: las 18 fichas, las 7 del catálogo, la portada del blog y contacto.
- GitHub Pages: estado «built», rama `main`, raíz.
- `curl -sI https://aclaborda1010101.github.io/central-culinaria-demo/` → 200, con `last-modified` del 18/09/2026. Responde; no se ha mirado en un navegador que se vea bien.
- `curl -sI https://aclaborda1010101.github.io/robots.txt` → 404: no hay `robots.txt` en la raíz del dominio.

## Bloqueos

- **La fuente no está en este repo.** Según la ficha de Lince, vive en un solo equipo y sin git: si se pierde, la web no se puede volver a generar. Desde aquí no se puede cambiar la web de forma reproducible.
- **La publicación borraría el mini cerebro.** Según la ficha de Lince, `deploy.mjs` (fuera del repo) empuja directo a `main` y borra todo lo que no sea lo compilado. La misma ficha dice que esa publicación no sobrevive al traspaso del repo a la organización. Si ese traspaso está previsto y cuándo: no consta.
- **Repo público y servido por Pages.** Al fusionar, `AGENTS.md`, `CLAUDE.md` y `ESTADO.md` quedan visibles también en la URL de la demo. Los `.md` no llevan `noindex`, así que un buscador podría indexarlos.
- **El `robots.txt` no protege en esta URL.** Queda bajo `/central-culinaria-demo/` y los buscadores solo lo leen en la raíz del dominio, donde no hay ninguno (ver «Pruebas»). Lo único que cierra la demo es el `noindex` de cada página.
- **El formulario no envía nada.** El destino (correo o CRM) está por decidir (ficha de Lince).
- **Fotos y vídeos provisionales**, servidos desde Unsplash y Pexels (ficha de Lince; visto en el HTML).
- **Contenido de ejemplo, sin validar.** Lo dicen las notas de «Prototipo» de las propias páginas: catálogo pendiente de validar con el catálogo real; datos de las 18 fichas (formatos, tiempos, ingredientes y alérgenos) pendientes de la ficha técnica real; portada del blog provisional, a falta de que el cliente defina su diseño.
- El teléfono (`+34 900 000 000`) parece de relleno. Si el resto de textos y el correo de contacto están validados por el cliente: no consta.

## Siguiente acción

Una persona decide qué hacer con el PR del mini cerebro, sabiendo que el repo es público y que Pages lo serviría.

Después, por orden (propuesta; no consta un plan acordado):

1. Subir la fuente a git.
2. Cambiar la publicación para que no borre `AGENTS.md`, `CLAUDE.md`, `ESTADO.md` ni `docs/`.
3. Leer el paquete anterior que cita la ficha de Lince y traer aquí lo que falte (ver el final de este fichero).

## Piezas reutilizables

Aquí solo está lo compilado; la fuente de cada pieza queda fuera del repo.

- Demo enseñable y cerrada a buscadores en GitHub Pages bajo `/<repo>/` — la etiqueta `noindex` de cada página. El `robots.txt` no vale bajo `/<repo>/` (ver «Bloqueos»).
- Notas de «prototipo» que se ocultan con `?notas=0` — guion en la cabecera de `index.html` y regla `.hide-notes .proto-note` en `assets/css/main.css`.
- Formulario que se rellena desde la URL (`motivo`, `perfil`, `producto`) — `assets/js/chunks/form-WFGZRJDY.js`.
- Efectos de scroll con GSAP y ScrollTrigger, y desplazamiento suave con Lenis, cargados por trozos bajo demanda — `assets/js/main.js` y `assets/js/chunks/`.
- Generador estático sin framework (`build.mjs`, con esbuild) — fuera de este repo, según la ficha de Lince.

Ficha del proyecto en Lince: `proyectos/central-culinaria.md`.

La ficha cita como fuentes un paquete anterior de este proyecto, fuera de este repo, con su propio `ESTADO.md` (01/10/2026) y su `AGENTS.md` (campo `fuentes` de la ficha). No se ha leído para este mini cerebro: puede traer estado o reglas que aquí no están.
