# Brief de contenido — Portfolio

Documento de trabajo: qué dice el sitio, con qué evidencia y por qué. Si algo
cambia en un proyecto, se actualiza acá primero y después se traduce a los
componentes.

Última actualización: 2026-10-24

---

## 1. Posicionamiento

- **Título:** Desarrollador Full Stack Jr. · Desarrollo asistido por IA.
- **Tesis:** especializo, dirijo y valido el trabajo de agentes; elijo
  harness, modelo y flujo según la tarea. No es "usar IA para escribir
  código": es diseñar el proceso, el contexto y la verificación.
- **Disponibilidad:** full time o part time; remoto o presencial en Mendoza.
- **Público:** pasantías y posiciones junior. Prioridad: equipos que ya
  trabajan con agentes o quieren hacerlo con criterio.
- **Datos públicos:** email, LinkedIn, GitHub y portfolio. El teléfono queda
  solo en el CV.

## 2. Flujo de trabajo con IA (fuente de la sección «IA aplicada»)

El flujo mutó por evidencia propia, no por adopción de moda:

1. **SDD completo** (spec → design → tasks → apply → verify) cuando el cambio
   lo justifica. En tareas chicas es sobreingeniería y quema tokens.
2. **Flujo actual:** un orquestador que, según la magnitud, resuelve él mismo,
   propone un plan y luego lanza subagentes, o delega directamente.
3. **Constante:** TDD siempre; verificación independiente cuando el change es
   grande; revisión del diff antes de aceptar.
4. **Slices:** porciones de funcionalidad probables de punta a punta, no capas
   a medio terminar.
5. **Contexto:** el mínimo suficiente (specs, AGENTS.md, estado del repo) en
   lugar de arrastrar la conversación completa.
6. **Costo por feature:** gasto por fase + lo que se ahorra al no rehacer
   trabajo. Se mide, no se estima.
7. **Modelos:** se prueban en tareas reales, no solo en benchmarks. Se asigna
   rol: orquestador, implementador, verificador, investigador.
8. **Origen:** el método base viene de gentle-ai; el resto es experiencia
   propia acumulada y ajustada.

### Harnesses (uso real)

| Herramienta | Uso |
|---|---|
| OpenCode + Pi | Desarrollo diario con SDD y ODD |
| Antigravity (`agy`) | Documentación y trabajos universitarios |
| Hermes | Tareas autónomas: investigación, navegador, operaciones en el sistema |

No se nombran marcas de modelos. Sí se afirma que se evalúan capacidades con
pruebas propias y se elige modelo por rol y costo.

## 3. Proyectos

### 3.1 agy-bridge — puente local OpenAI-compatible

- Open source (MIT), TypeScript + Deno + Docker + GitHub Actions.
- Expone los modelos de la suscripción de Antigravity como API OpenAI para
  cualquier cliente (opencode en particular).
- Invariante: todo el tráfico lo hace el binario oficial `agy` en headless con
  su propia auth; el bridge no lee ni copia credenciales, no hace OAuth propio.
- Seguridad: bind loopback, Bearer token, guard anti-DNS-rebinding.
- Tres perfiles de agente: `raw` (escape hatch), `worker-ro`, `worker-rw`.
- Catálogo dual OpenCode V1/V2: el instalador detecta la versión y escribe la
  forma nativa de cada runtime.
- Instalador Linux (systemd --user) + Docker Compose para Windows. CI con
  verificación determinista.
- Medición propia: ~7,4k tokens de overhead por tarea autónoma en solo lectura
  y ~9,8k en lectura/escritura; ~40k por turno en modo stateless. Ese dato
  define cuándo delegar en modo autónomo.
- Evidencia: 80 tests (`deno task test`), 19/19 checks del smoke de plugin V2,
  14 modelos en el catálogo, 42 commits y 20 PRs.

Links: repo público <https://github.com/AlvaroTapia-f/agy-bridge>. Sin demo
ejecutable (es una herramienta local). Imagen: diagrama de arquitectura propio.

### 3.2 Álbum de Películas — app privada para dos

- En producción: <https://album-peliculas-digital.vercel.app>
- SvelteKit 2 + Svelte 5 (runes), TypeScript, Tailwind 4, Supabase
  (PostgreSQL), TMDB API, Vercel. Repo privado.
- Producto: álbum tipo libro, reseñas con puntaje compartido, watchlist,
  timeline, estadísticas y juego de Match para decidir qué ver.
- Decisión central: la autorización vive en la base. RLS de PostgreSQL con
  `auth_couple_id()` `SECURITY DEFINER`; sin backend propio de auth, la
  `anon key` puede vivir en el browser.
- Proxy server-side para TMDB: la API key nunca llega al cliente.
- Capas estrictas: rutas → services → componentes.
- Match con Supabase Realtime: dos pantallas avanzan juntas sobre un estado
  persistido en la base.
- PWA instalable con shell offline.
- Evidencia: 112 tests (Vitest + Playwright), 91,8% statements, 82/82
  escenarios de spec, 42 entradas precacheadas, 5 changes con SDD y 21
  decisiones documentadas (D1–D21).
- Capturas: `album-grid.webp` (principal), `album-match.webp`,
  `album-stats.webp`, `album-add.webp`.

## 4. Skills

Categorías: **IA y agentes** (OpenCode, Pi, Antigravity, Hermes, SDD, ODD,
subagentes, verificación independiente, gestión de contexto y costo, TDD,
guardrails), **Lenguajes y backend** (TypeScript, JavaScript, Java, Python,
SQL, Node.js, Express, Spring Boot, APIs REST), **Frontend** (Svelte, React,
Astro, HTML, CSS, Tailwind), **Datos** (PostgreSQL, Supabase, MongoDB, RLS,
RPC), **DevOps y herramientas** (Git, GitHub Actions, Docker, Linux, Vercel,
Vitest, Playwright, Postman, Swagger).

## 5. Educación

- Ingeniería en Sistemas de Información — UTN-FRM, 2022 – actualidad.
  27 de 36 materias aprobadas, cursando 4.º y 5.º año.
- Electivas: Modelos de Lenguajes (cursando), Bases de Datos Avanzadas
  (cursando), Administración de Proyectos (8 hs).
- Técnico Electromecánico — Escuela Ing. Pablo Nogués, 2016 – 2021.

## 6. Decisiones de sitio

- Un solo idioma: español. `<html lang="es">`.
- Se mantiene la estética: Roboto Mono, fondo punteado, paleta violeta,
  dark/light por `prefers-color-scheme`.
- CV descargable desde `public/Alvaro_Tapia_CV.pdf`.
- Sin sección de experiencia laboral (decisión del autor); la trayectoria
  laboral vive en el CV.
- Repo del Álbum privado: se muestra como «código privado, disponible a pedido».
