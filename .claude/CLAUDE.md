# portfolio · CLAUDE.md

Web pública de Pablo en GitHub Pages: https://pablofriascampos.github.io/portfolio/
Un solo `index.html`, sin build ni dependencias (salvo Google Fonts, ver POR-3). Se trabaja en **español de España**.

> Este archivo vive en `.claude/` a propósito: GitHub Pages (Jekyll) ignora las carpetas que empiezan por punto, así que **no se publica**. No lo muevas a la raíz.

## Qué construimos
- La web habla primero a **clientes** (negocios con cita y atención al público), no a reclutadores: «Tu WhatsApp responde aunque estés atendiendo». Secciones: hero, empresas, lo que he construido, servicios, caso, cómo trabajo, quién soy, contacto.
- Rehecha en POR-1 (PR #1, 15-nov-2026). Tareas abiertas y su estado: en el HQ (`hq tareas listar --proyecto portfolio`).

## Reglas duras
- **Publicar = merge a `main`** (GitHub Pages despliega solo). Merge solo con OK explícito de Pablo, tras ver capturas a 1440 y 390 px. Squash, para que las capturas de revisión no queden en la historia.
- **Nada de cifras inventadas.** Resultados solo reales y con permiso.
- **Caso de la clínica, anónimo**: «Clínica de fisioterapia en Málaga». Sin nombre, sin capturas con datos reales, sin testimonios inventados. Lleva la línea de estado «construido y probado; puesta en marcha en curso» hasta que esté en producción.
- **Freepik**: Pablo participó en el CRM de Magnific (antes Freepik) en el equipo de Adrián Martín. Puede citar su participación, **nunca las cifras de ese caso como propias**.
- **Job&Talent** (Salesforce Analyst, mar 2026–hoy) sí se muestra. Nada sobre gestionar equipo hasta que Pablo lo diga.
- Fuera: Pokedex, GitHub y cualquier referencia a repositorios. Contacto: email `pablofriascampo@gmail.com` (correcto, sin «s») y LinkedIn.
- Las capturas de revisión **no** se quedan en el repo: se commitean para la PR y se quitan en el commit siguiente.
- Servidor local de pruebas en `127.0.0.1`, nunca `0.0.0.0`.

## Diseño
Referencia de calidad (sin copiarla): https://www.adrianmartin.me/. Titular gigante en grotesca muy negrita (Bricolage Grotesque 800), frases humanas en Instrument Serif cursiva, secciones alternando oscuro y claro, **un solo acento** (coral `#ff6a3d`), retrato en blanco y negro (`assets/pablo.jpg`, pendiente: POR-4), CTA claro. Nada de estética de terminal.

## Cómo trabajar (operativa)
| Quiero… | Cómo |
|---|---|
| Ver la web en local | `npx serve -l tcp://127.0.0.1:4590 .` o `python -m http.server 4590 --bind 127.0.0.1` |
| Validar | Sin tests: HTML bien formado, consola sin errores, sin scroll horizontal y anclas que funcionan, a 1440 y 390 px |
| Ver las tareas | MCP `hq` → `tareas_listar` / `tarea_ver POR-<n>`; o `node C:/Users/P4/orca/projects/hq/bin/hq.js tareas listar --proyecto portfolio` |
| Ver si Pages desplegó | `gh run list -L 2` (workflow «pages build and deployment») |

## Coordinación con el HQ, agentes y worktrees
El repo **no tiene `hq.json`**, así que no se aplican las skills `/hq-*` al pie de la letra. Pero las tareas se registran en el HQ (proyecto `portfolio`, clave **POR**) y, cuando compensa, se trabaja con coordinador + workers igual que en el resto de proyectos.
- **El HQ** (`C:/Users/P4/orca/projects/hq`) manda en las tareas: `tarea_crear`, `tarea_actualizar` (notas y decisiones de Pablo), `tarea_mover` (estado). Antes de investigar algo, busca en su conocimiento (`conocimiento_buscar`). Nunca edites a mano `datos/*.jsonl` ni escribas en el repo del HQ desde aquí: propón el cambio.
- **Coordinador** = la sesión en este checkout principal (`main`). Habla con Pablo, lanza workers, revisa PRs y mergea con su OK. **No implementa en `main`**. Excepción: retoques triviales de docs como este archivo, también con OK de Pablo para el push.
- **Worker** = un worktree de Orca por tarea, siempre desde `main`, rama `feat-por-<n>-<slug>` y PR `[POR-<n>] …`. Se lanza con `tarea_lanzar` del MCP `hq` (comprueba conflictos), tras enseñar el brief (`tarea_brief`) y con OK de Pablo. Alternativa: `orca worktree create --name feat-por-<n>-<slug> --no-parent --agent claude --prompt "<brief>"`.
- **Avisos**: el worker no pregunta en su terminal. Busca al coordinador con `ListAgents` (sesión `portfolio-…`) y le escribe por `SendMessage`, con la primera línea `[POR-<n>] <qué pasa>`. Avisa al abrir la PR, si necesita una decisión, si se bloquea y al terminar. El coordinador resume para Pablo y le devuelve su respuesta.
- **Seguimiento**: `ListAgents` (ocupado o libre), `git worktree list`, `gh pr list`. Para enterarte de cuándo termina un worker usa `SendMessage` con `notify_when_idle`; no hagas sondeos en bucle.
- **Cierre**: OK de Pablo → `gh pr merge <n> --squash --match-head-commit <sha>` → `git pull --ff-only` → comprobar el despliegue de Pages → `tarea_mover POR-<n> hecha` → avisar al worker. Borrar el worktree y la rama (`orca worktree rm`, `git branch -d`, rama remota) **solo con OK de Pablo**.
- Paralelo: casi todo toca `index.html`, que es **cuello de botella**. Un worker cada vez.
- Detalle del método: `conocimiento/metodo/` del HQ (`coordinador-y-workers.md`, `brief-de-worker.md`, `avisos-sendmessage.md`, `cierre-de-tarea.md`).

## Acciones hacia fuera (siempre con OK explícito de Pablo; un «sí» no se hereda)
Push a `main`, merges, borrados (ramas, worktrees, archivos publicados), descargar recursos de terceros (fuentes, imágenes), crear repos o recursos externos y enviar mensajes a personas reales.

## Definición de hecho
Página validada a mano a 1440 y 390 px · sin secretos ni datos personales de clientes finales · sin cifras inventadas · PR pequeña con resumen, «cómo revisar» y capturas (quitadas después).
