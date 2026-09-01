# Adapter: Godot Engine

> Activar cuando el proyecto use **Godot 4.x**.  
> Complementa las reglas genéricas de `core/` con convenciones y patrones específicos de Godot.

---

## Identificación del proyecto

El agente debe activar este adapter si detecta cualquiera de:
- Archivo `project.godot` en la raíz del repo de juego.
- Extensiones `.tscn`, `.gd`, `.tres`, `.gdshader` en el código fuente.
- Carpeta `res://` referenciada en rutas.

---

## Estructura de proyecto canónica

```
game/
  client/                  ← raíz del proyecto Godot
    project.godot
    icon.svg
    scripts/               ← GDScript (.gd)
      autoloads/           ← Singletons globales
      entities/            ← Lógica de entidades del juego
      ui/                  ← Controladores de UI
      utils/               ← Helpers y extensiones
    scenes/                ← Escenas (.tscn)
      ui/
      world/
      entities/
    resources/             ← Recursos compartidos (.tres)
    shaders/               ← Shaders (.gdshader)
    assets/
      sprites/
      audio/
      fonts/
```

---

## Convenciones de código (GDScript)

### Nomenclatura

| Elemento | Convención | Ejemplo |
|---|---|---|
| Clase / Script | `PascalCase` | `PlayerController.gd` |
| Variable | `snake_case` | `health_points` |
| Constante | `UPPER_SNAKE` | `MAX_SPEED` |
| Señal | `snake_case` (verbo pasado) | `player_died`, `item_collected` |
| Función privada | `_snake_case` | `_on_body_entered()` |
| Nodo autoload | `PascalCase` | `GameManager`, `AudioBus` |

### Límite de líneas por archivo

| Tipo | Límite |
|---|---|
| Script de entidad | ≤ 150L |
| Script de UI | ≤ 100L |
| Autoload / Singleton | ≤ 200L |
| Script de utilidad | ≤ 80L |

> Si un script supera su límite → flag `[deuda: split script]` en `overview/work/deuda_tecnica.md`.

---

## Patrones arquitectónicos

### Señales sobre referencias directas

```gdscript
# ✅ Correcto — desacoplado
signal health_changed(new_value: int)

# ❌ Evitar — acoplamiento directo
$UI/HealthBar.update(health)
```

### Autoloads (Singletons globales)

Usar **solo** para estado verdaderamente global:
- `GameManager` — estado de partida, escena activa
- `AudioBus` — control de audio global
- `EventBus` — señales inter-escena

> Máximo **4 autoloads** activos. Si se necesita más, revisar si el estado es realmente global.

### SceneTree como arquitectura

```
Main (Node)
  ├── World (Node2D / Node3D)
  │     └── Entidades...
  ├── UI (CanvasLayer)
  │     └── HUD, Menús...
  └── GameManager (Autoload)
```

---

## Comandos específicos de Godot

### `$archi` — extensiones Godot

Además del protocolo base, el agente debe incluir en `overview/architecture/routes_map.md`:

```markdown
## SceneTree Map
- Main.tscn → escena raíz
- World.tscn → mapa/nivel activo
- UI.tscn → capa de interfaz
```

Y en `overview/architecture/core/data_flow.md`:
- Listar todos los Autoloads registrados en `project.godot`
- Documentar señales inter-escena del `EventBus`

### `$close` — validación Godot

En lugar de `flutter analyze`, ejecutar:
```bash
# Verificar errores de parseado de GDScript (si está disponible)
godot --headless --quit 2>&1 | grep -i error
```
Si Godot CLI no está disponible → reportar `validación: no aplica (CLI ausente)`.

---

## Anti-patrones específicos de Godot

| Anti-patrón | Problema | Solución |
|---|---|---|
| `get_node()` con rutas largas | Frágil ante renombrado | Usar `@onready var` o señales |
| Lógica de juego en `_process()` | Acoplado al frame rate | Usar `_physics_process()` o señales |
| Escenas monolíticas (+50 nodos) | Difícil de mantener | Dividir en sub-escenas instanciadas |
| Autoloads para estado local | Contamina el scope global | Pasar datos por señales o recursos |
| `print()` en producción | Overhead en builds | Usar `push_warning()` / `push_error()` |

---

## Integración con el ecosistema

- **Lore Skill** (`.skills/lore-agent-skill`): usar para entidades narrativas del mundo del juego.
- **`$archi`**: genera `routes_map.md` con el SceneTree documentado.
- **`overview/learning.md`**: abstraer aprendizajes de Godot a reglas agnósticas antes de registrar.
