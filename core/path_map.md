# Mapa canónico de rutas (Godot & Game Lore)

## Reglas globales: submódulo `.agents/`

| Recurso | Ruta | Carga |
|---|---|---|
| Comunicación | `.agents/core/communication.md` | Obligatoria — **leer primero** |
| Router | `.agents/AGENTS.md` | Obligatoria |
| Brain | `.agents/core/brain.md` | Obligatoria |
| Comandos | `.agents/core/commands.md` | Obligatoria |
<<<<<<< HEAD
| Conocimiento Godot | `.agents/knowledge/godot_structure.md` | Bajo demanda |
| Conocimiento Lore | `.agents/knowledge/lore_architecture.md` | Bajo demanda |
| Estilo de Código | `.agents/knowledge/code_style.md` | Bajo demanda |
| Plantillas | `.agents/templates/` | Al iniciar |
| Skills Game Dev | `.agents/skills/godot-game-dev/` | Bajo demanda |
=======
| Adaptadores (Codex / Cursor / etc) | `.agents/adapters/` (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `cursor-rule.mdc`, `README.md`) | Al instalar |
| Estructura Flutter | `.agents/knowledge/flutter_structure.md` | Discovery |
| Estilo Dart / Clean Arch | `.agents/knowledge/code_style.md` | Bajo demanda |
| Arquitectura Base | `.agents/knowledge/architecture.md` | Bajo demanda |
| Release Checklist | `.agents/knowledge/release_checklist.md` | `$close` / Build |
| Plantillas `overview/` | `.agents/templates/` | `$boot` / Inicio |
| Skill Clean Arch & Limits | `.agents/skills/flutter-clean-arch/SKILL.md` | Refactors / UI |
| Skill Diagrams Mermaid | `.agents/skills/mermaid-diagrams/SKILL.md` | Diagramación |
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

## Estado local: raíz del proyecto

| Recurso | Ruta | Carga |
|---|---|---|
| Sesión | `overview/session.md` | Inicio/cierre |
<<<<<<< HEAD
| Trabajo / Backlog | `overview/work.md` | Inicio/cierre |
| Aprendizajes | `overview/learning.md` | Al cerrar |
| Arquitectura Godot | `overview/architecture.md` | Al iniciar |
| Progreso | `overview/trackers/progress.md` | Inicio/cierre |
=======
| Trabajo (Índice Maestro) | `overview/work.md` | Inicio/cierre |
| Tarea Activa | `overview/work/tasks.md` | Inicio/en ejecución |
| Pendientes | `overview/work/pendientes.md` | Cierre/bajo demanda |
| Deuda Técnica | `overview/work/deuda_tecnica.md` | Inicio/bajo demanda |
| Protocolo Revisión Work | `overview/work_review.md` | Fin de `$boot` |
| Aprendizajes | `overview/learning.md` | Al cerrar |
| Arquitectura real | `overview/architecture.md` | Al iniciar |
| Tracker Arquitectura | `overview/trackers/architecture.md` | Bajo demanda |
| Tracker Progreso | `overview/trackers/progress.md` | Inicio/cierre |
| Contenido | `overview/trackers/content_*.md` | Si aplica |
| Modularización Contenido | `overview/trackers/content/<cat>/<item>.md` | Bajo demanda |
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17
| Historial | `overview/history/` | Al resumir |
| Contexto de agente | `overview/context/` | Inicio/bajo demanda |
| Flujos de agente | `overview/workflows/` | Bajo demanda |

<<<<<<< HEAD
## Documentación viva del proyecto / Lore: `docs/`

| Recurso | Ruta | Carga |
|---|---|---|
| **Arbol Narrativo** | `docs/lore/narrative_tree.md` | Inicio/Bajo demanda |
| **Worldbuilding** | `docs/lore/worldbuilding.md` | Bajo demanda |
| **Personajes** | `docs/lore/characters.md` | Bajo demanda |
| **Misiones / Quests** | `docs/lore/quests.md` | Bajo demanda |
| **Diálogos / Nodos** | `docs/lore/dialogues.md` | Bajo demanda |
| **Facciones / Matrices**| `docs/lore/factions.md` | Bajo demanda |
| **GDD / Diseño** | `docs/gdd/` | Bajo demanda |

> [!IMPORTANT]
> **Separación estricta de responsabilidades**: `overview/` es un espacio exclusivo para el estado interno y control del agente (`session.md`, `work.md`, `trackers/`, etc.). La documentación viva del proyecto, GDD y lore deben alojarse en `docs/` para evitar contaminación de la taxonomía del agente.

> `docs/lore/` contiene la arquitectura viva de la historia del proyecto: mapa de nodos narrativos, worldbuilding, relaciones de facciones, fichas de personajes, misiones principales/secundarias y árboles de diálogo que conectan con los scripts/recursos (`.tres`) de Godot.

> `overview/context/` conserva archivos suplementarios (concept art markdown, bibliografía del lore, notas de producción, changelogs narrativos).

> `overview/architecture.md` refleja la estructura técnica en Godot: Árbol de Nodos, Escenas (`.tscn`), Autoloads/Singletons, Máquinas de Estado (FSM), Sistema de Eventos/Señales, y Recursos (`.tres`).
=======
> `overview/context/` es para archivos de dominio no mapeables al framework ni al estado de sesión: contexto general, changelogs de contenido, datos de referencia de la app. Se leen al reanudar como checkpoints.

> `overview/workflows/` es la **ubicación canónica** para registrar guías de dominio por flujo en términos agnósticos (ej. materia prima: `Entrada → Inventario → Producción`). Se mantiene estrictamente separada de `overview/architecture.md` (mapa de arquitectura técnica de código) y de `overview/context/` (datos de negocio / archivos de referencia general).
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

### Backlog canónico único y Prioridad de atención

<<<<<<< HEAD
- `overview/work.md` = **única** tabla de IDs (`tarea` / `bug` / `deuda` / `lore`).
- Detalle de tareas narrativas o técnicas: filas en `work.md` con tag `[gameplay]` o `[lore]`.
- Alias `tasks.md` → solo redirección; **nunca** duplicar backlog ahí.
=======
- `overview/work.md` = **único** índice y tabla maestra de IDs (`tarea` / `bug` / `deuda`).
- **Orden de prioridad de atención en `$work`**:
  1. `overview/work/tasks.md` (tarea activa en ejecución)
  2. `overview/work/pendientes.md` (ítems de seguimiento identificados)
  3. `overview/work/deuda_tecnica.md` (deuda ordenada por prioridad **Alta**, **Media** y **Baja**)
- **Histórico de completados**: Todas las tareas, pendientes y deudas resueltas deben trasladarse a `## ✅ Completados (Historial)` conservando su ID correspondiente (`[w1]`, `[d2]`, `[p1]`).
- No duplicar detalles en el alias heredado `tasks.md` ni escribir backlogs paralelos fuera del esquema canónico.
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

## Alias heredados

| Alias | Ruta actual |
|---|---|
<<<<<<< HEAD
| `overview/tracker.md` | `overview/architecture.md` |
| `overview/tasks.md` | `overview/work.md` |
| `memory_session.md` | `overview/session.md` |

> Si coexisten alias y canónico con contenido distinto → flag consolidación obligatorio (`brain.md`). Nunca asumir cuál manda sin verificar.

=======
| `overview/tracker.md` | `overview/trackers/architecture.md` |
| `overview/tasks.md` (raíz) | `overview/work.md` / `overview/work/tasks.md` |
| `memory_session.md` | `overview/session.md` |

> Si coexisten alias y canónico con contenido distinto (ej. `tasks.md`/`work.md` o `tracker.md`/`trackers/architecture.md`) → flag `[consolidar alias]` obligatorio (`brain.md`). Nunca asumir cuál manda sin verificar diff previo.
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17
