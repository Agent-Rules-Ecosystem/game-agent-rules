# Mapa canónico de rutas (Godot & Game Lore)

## Reglas globales: submódulo `.agents/`

| Recurso | Ruta | Carga |
|---|---|---|
| Comunicación | `.agents/core/communication.md` | Obligatoria — **leer primero** |
| Router | `.agents/AGENTS.md` | Obligatoria |
| Brain | `.agents/core/brain.md` | Obligatoria |
| Comandos | `.agents/core/commands.md` | Obligatoria |
| Conocimiento Godot | `.agents/knowledge/godot_structure.md` | Bajo demanda |
| Conocimiento Lore | `.agents/knowledge/lore_architecture.md` | Bajo demanda |
| Estilo de Código | `.agents/knowledge/code_style.md` | Bajo demanda |
| Plantillas | `.agents/templates/` | Al iniciar |
| Skills Game Dev | `.agents/skills/godot-game-dev/` | Bajo demanda |

## Estado local: raíz del proyecto

| Recurso | Ruta | Carga |
|---|---|---|
| Sesión | `overview/session.md` | Inicio/cierre |
| Trabajo / Backlog | `overview/work.md` | Inicio/cierre |
| Aprendizajes | `overview/learning.md` | Al cerrar |
| Arquitectura Godot | `overview/architecture.md` | Al iniciar |
| Progreso | `overview/trackers/progress.md` | Inicio/cierre |
| Historial | `overview/history/` | Al resumir |
| Contexto de agente | `overview/context/` | Inicio/bajo demanda |
| Flujos de agente | `overview/workflows/` | Bajo demanda |

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

### Backlog canónico único y Prioridad de atención

- `overview/work.md` = **única** tabla de IDs (`tarea` / `bug` / `deuda` / `lore`).
- Detalle de tareas narrativas o técnicas: filas en `work.md` con tag `[gameplay]` o `[lore]`.
- Alias `tasks.md` → solo redirección; **nunca** duplicar backlog ahí.

## Alias heredados

| Alias | Ruta actual |
|---|---|
| `overview/tracker.md` | `overview/architecture.md` |
| `overview/tasks.md` | `overview/work.md` |
| `memory_session.md` | `overview/session.md` |

> Si coexisten alias y canónico con contenido distinto → flag consolidación obligatorio (`brain.md`). Nunca asumir cuál manda sin verificar.

