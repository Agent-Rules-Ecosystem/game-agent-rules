# Estructura Estándar de Proyecto Godot Engine (Godot 4+)

Este documento especifica la estructura de carpetas, escenas y scripts nativos estándar reconocidos en un proyecto Godot 4.

## Directorios Estándar de Godot Engine

| Directorio | Propósito | Tratamiento |
|---|---|---|
| `scenes/` o `res://scenes/` | Escenas `.tscn` (Niveles, Personajes, UI, Objetos) | Conservar en root |
| `scripts/` o `res://scripts/` | Archivos de código GDScript `.gd` | Conservar en root |
| `resources/` o `res://resources/` | Recursos personalizados `.tres` (Stats, Items, Quests) | Conservar en root |
| `autoload/` o `res://autoload/` | Singletons globales (EventBus, GameState, Audio, LoreManager) | Conservar en root |
| `assets/` o `res://assets/` | Texturas, sprites, modelos 3D, sonidos, música, fuentes | Conservar en root |
| `.godot/` | Metadata de compilación e importación de Godot 4 | Ignorar en discovery |
| `.agents/` | Submódulo oficial de reglas compartidas de juego | Conservar en root |
| `overview/` | Estado local versionado del proyecto y arquitectura de juego | Conservar en root |
| `overview/lore/` | Mapeo de la historia, arbol narrativo, misiones y personajes | Conservar en root |

## Archivos Estándar en Root

- `project.godot` (Archivo maestro del proyecto Godot)
- `export_presets.cfg` (Configuración de exportación)
- `icon.svg` / `icon.png` (Icono del proyecto)
- `.gitignore`, `README.md`, `LICENSE`

## Patrones de Arquitectura de Juego en Godot

1. **Composición de Nodos vs Herencia**:
   - Preferir agregar componentes como nodos hijo (`HealthComponent`, `HitboxComponent`, `HurtboxComponent`, `StateMachine`) en lugar de herencia profunda de clases.
2. **Patrón EventBus (Señales Globales)**:
   - Crear un singleton en `autoload/event_bus.gd` para emitir eventos globales (`player_health_changed`, `quest_completed`, `dialogue_started`).
3. **Data-Driven con Resources (`.tres`)**:
   - Crear clases que hereden de `Resource` (ej. `class_name ItemData extends Resource`) para definir items, diálogos o misiones sin hardcodear datos en scripts.
4. **Desacoplamiento UI-Gameplay**:
   - Las interfaces de usuario escuchan eventos del EventBus y actualizan sus elementos sin modificar el estado directamente.
