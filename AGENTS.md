---
name: game-agent-rules
description: Bootstrap y gobernanza para agentes de IA en proyectos de desarrollo de juegos con Godot 4 y documentación de Lore/Narrativa.
---

# Game Dev & Lore Agent Rules (Godot 4)

## Bootstrap obligatorio

Antes de responder o editar, leer y cumplir:

1. `.agents/core/communication.md` ← **primero siempre; rige todo lo que sigue**
2. `.agents/core/path_map.md`
3. `.agents/core/brain.md`
4. `.agents/core/commands.md`

**Triggers de arranque** — las siguientes frases o condiciones disparan el protocolo completo:

- **"ejecuta .agents"** (o "corre .agents", "bootstrap .agents") → dispara el Protocolo de Auditoría de Learning.
- "nuevo juego" / "nuevo lore" / "inicializar godot" / "bootstrap" / "empieza" en el primer mensaje.
- Ausencia de `overview/session.md` al comenzar cualquier tarea de código GDScript o mapeo de lore.
- Primer mensaje de conversación cuando el proyecto tiene `.agents/` pero no `overview/`.
- Cualquier mensaje que comience con `$` → reconocer como $-comando según `core/commands.md`.

Para cualquier tarea que inspeccione o cambie código GDScript (`.gd`, `.tscn`), escenas o documentos de historia/lore, cargar `overview/session.md`, `overview/work.md`, `overview/work/tasks.md`, `overview/work/deuda_tecnica.md`, `overview/work/pendientes.md` y `overview/trackers/progress.md`. Actualizar todos los archivos de control en `overview/` de forma automática y simultánea durante `$work` y `$close`. Si falta `overview/` o uno de esos archivos, crearlo desde `.agents/templates/`. Al finalizar `$boot`, ejecutar el protocolo `overview/work_review.md`.

Las reglas globales viven solo en `.agents/`. **Inviolabilidad estricta de `.agents/`**: Nunca modificar directamente archivos de gobernanza desde un proyecto local.

## Estado local versionado

Crear `overview/` desde `.agents/templates/` al iniciar proyecto. Al inicio y cierre, cargar/actualizar:

- `overview/session.md`
- `overview/work.md` (índice maestro)
- `overview/work/tasks.md` (tarea activa: tipo, solución/rutas)
- `overview/work/pendientes.md` (seguimiento al cerrar)
- `overview/work/deuda_tecnica.md` (deuda ordenada por prioridad Alta, Media y Baja)
- `overview/work_review.md` (protocolo de auditoría `$boot`)
- `overview/workflows/` (guías por flujo con terminología 100% agnóstica)
- `overview/trackers/progress.md`
- `overview/trackers/architecture.md` cuando aplique (actualizable vía `$archi` con diagramas Mermaid)
- `overview/architecture.md` (Estructura de Escenas, Autoloads, Nodos y Sistemas Godot)
- `docs/lore/` (Árbol Narrativo, Misiones, Personajes, Worldbuilding, Diálogos)
- `overview/context/` para archivos de contexto general no mapeables
- `overview/learning.md` cuando surja mejora candidata (propuestas al core)

> **Separación estricta**: `overview/` es exclusivo para el estado interno del agente. Documentación y lore deben alojarse en `docs/`.

`overview/history/` conserva sesiones antiguas. Cambios a reglas globales solo ocurren en repositorio oficial con aprobación del propietario.
