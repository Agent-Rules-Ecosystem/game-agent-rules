# Estilo de Código GDScript 2.0 y Convenciones en Godot 4

## GDScript y Archivos

- **Tipado Estático Obligatorio**: Usar siempre anotaciones de tipo (`var health: int = 100`, `func heal(amount: int) -> void:`).
- **Límite de Líneas**: Mantener scripts `.gd` idealmente bajo 250 líneas; máximo 300 líneas. Extraer componentes a nodos hijo o Recursos (`.tres`).
- **Nodos y `@onready`**: Inicializar referencias a nodos hijo usando `@onready var sprite: Sprite2D = $Sprite2D`.
- **Señales**: Definir señales en la parte superior del script con tipos explícitos (`signal health_changed(new_health: int)`).

## Nombrado y Convenciones

| Elemento | Convención | Ejemplo |
|---|---|---|
| Clases / `class_name` | `PascalCase` | `class_name PlayerController` |
| Archivos GDScript | `snake_case` | `player_controller.gd` |
| Archivos de Escenas | `snake_case` | `main_menu.tscn` |
| Variables / Métodos | `snake_case` | `var move_speed: float = 200.0`, `func take_damage()` |
| Constantes | `ALL_CAPS_SNAKE` | `const MAX_HEALTH: int = 100` |
| Señales | `snake_case` (pasado) | `signal player_died`, `signal item_collected(item)` |
| Enums | `PascalCase`, valores `ALL_CAPS` | `enum State { IDLE, RUN, ATTACK }` |

## Patrones de Código en Godot

1. **"Call Down, Signal Up"**:
   - Los nodos superiores llaman a métodos del hijo (`$Weapon.attack()`).
   - Los nodos inferiores emiten señales hacia arriba (`signal_hit.emit()`).
2. **Máquina de Estados (State Machine)**:
   - Encapsular estados en scripts o nodos heredados de `State`. Evitar `if/elif/else` gigantes en `_process` o `_physics_process`.
3. **EventBus Centralizado (Autoload)**:
   - Usar `EventBus.gd` para eventos globales del juego que conectan sistemas desacoplados (Gameplay ↔ UI ↔ Lore Manager).
4. **Resources (`.tres`) para Datos**:
   - Definir datos de items, estadísticas y misiones en subclases de `Resource`. Cargar con `preload()` o `load()`.
