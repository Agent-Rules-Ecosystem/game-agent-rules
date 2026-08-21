# Estilo y Convenciones de GDScript 4

## Nomenclatura

| Elemento | Convención | Ejemplo |
|---|---|---|
| Clases / Nodos | `PascalCase` | `PlayerController`, `EnemyAI` |
| Archivos `.gd` | `snake_case` | `player_controller.gd` |
| Variables / funciones | `snake_case` | `get_player_health()` |
| Constantes | `UPPER_SNAKE_CASE` | `MAX_SPEED`, `DEFAULT_HEALTH` |
| Señales | `snake_case` como verbos pasados | `health_changed`, `enemy_died` |
| Enums | `PascalCase`, valores `ALL_CAPS` | `enum State { IDLE, RUNNING, JUMPING }` |

## Tipado Estático (Obligatorio)

- Siempre tipar variables: `var speed: float = 5.0` en lugar de `var speed = 5.0`.
- Siempre tipar retorno de funciones: `func get_health() -> int:`.
- Preferir `@onready var sprite: Sprite2D = $Sprite2D` para referencias a nodos.
- Usar `@export var speed: float = 5.0` para variables configurables desde el editor.

## Señales y Desacoplamiento

- Preferir señales sobre referencias directas entre nodos de distintos niveles del árbol.
- Conectar señales en `_ready()`, desconectarlas en `_exit_tree()`.
- Nunca usar `get_node("../../OtroNodo")` con rutas relativas frágiles.

## Límite de Archivo

- Scripts idealmente < 250 líneas; máximo 300.
- Scripts > 300L → candidato a deuda técnica (`deuda_tecnica.md`).
- Extraer lógica en componentes hijos o `Resource` cuando sea posible.
