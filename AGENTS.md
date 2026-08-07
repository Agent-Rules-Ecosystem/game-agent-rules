---
name: agent-rules-governance
description: Bootstrap y gobernanza para reglas de agente de Desarrollo de Juegos en Godot y Mapeo de Historia/Lore.
---

# Game Dev & Lore Agent Rules (Godot Engine)

## Bootstrap obligatorio

Antes de responder o editar, leer y cumplir:

1. `.agents/core/communication.md` ← **primero siempre; rige todo lo que sigue**
2. `.agents/core/path_map.md`
3. `.agents/core/brain.md`
4. `.agents/core/commands.md`

**Triggers de arranque** — las siguientes frases o condiciones disparan el protocolo completo (discovery de Godot/Lore + `overview/` + mapeo de narrativa y código):

- **"ejecuta .agents"** (o "corre .agents", "bootstrap .agents") → dispara además el Protocolo de Auditoría de Learning definido en `brain.md`.
- "nuevo juego" / "nuevo lore" / "inicializar godot" / "bootstrap" / "empieza" en el primer mensaje.
- Ausencia de `overview/session.md` al comenzar cualquier tarea de código GDScript o mapeo de lore.
- Primer mensaje de conversación cuando el proyecto tiene `.agents/` pero no `overview/`.
- Cualquier mensaje que comience con `$` → reconocer como $-comando según `core/commands.md` y ejecutar el protocolo correspondiente.

Para cualquier tarea que inspeccione o cambie código GDScript (`.gd`, `.tscn`), escenas o documentos de historia/lore, cargar previamente `overview/session.md`, `overview/work.md` y `overview/trackers/progress.md`. Actualizar `overview/work.md` y `overview/session.md` INMEDIATAMENTE antes de ejecutar (Registro preventivo previo a ejecución); en reporte de bug incluir hipótesis breve (5-7 palabras). Si falta `overview/` o uno de esos archivos, crearlo desde `.agents/templates/`. Si falta `overview/architecture.md` o la carpeta `overview/lore/`, crearlos desde sus plantillas correspondientes.

Las reglas globales viven solo en `.agents/`. Si el agente no descubre `.agents/AGENTS.md`, instalar adaptador mínimo desde `.agents/adapters/`; nunca duplicar reglas. Al editar este repositorio oficial directamente, usar rutas locales equivalentes (`core/`, `templates/`, etc.).

## Estado local versionado

Crear `overview/` desde `.agents/templates/` al iniciar proyecto de juego. Al inicio y cierre, cargar/actualizar:

- `overview/session.md`
- `overview/work.md`
- `overview/trackers/progress.md`
- `overview/architecture.md` (Estructura de Escenas, Autoloads, Nodos y Sistemas Godot)
- `overview/lore/` (Arbol Narrativo, Misiones, Personajes, Worldbuilding, Diálogos)
- `overview/context/` para archivos de dominio o bibliografía del mundo no mapeables
- `overview/learning.md` cuando surja mejora candidata

`overview/history/` conserva sesiones antiguas. Cambios a reglas globales solo ocurren en repositorio oficial con aprobación del propietario.

