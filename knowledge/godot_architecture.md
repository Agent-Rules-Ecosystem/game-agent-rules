# Arquitectura de Proyectos Godot 4

## Principios de Arquitectura de Nodos

| Principio | Descripción |
|---|---|
| **Composición sobre herencia** | Preferir componentes hijo (`HealthComponent`, `HitboxComponent`) sobre herencia profunda. |
| **Signal Bus desacoplado** | Autoload global `EventBus.gd` para comunicación entre sistemas sin referencias directas. |
| **Resource como dato** | Usar archivos `.tres` para estadísticas, configuraciones e ítems (desacoplados del código). |
| **Scene boundaries** | Cada escena es autónoma; no depende de la jerarquía del árbol padre. |

## Capas de Arquitectura

| Capa | Responsabilidad | Nodos/Recursos |
|---|---|---|
| **Presentación** | Visual y animaciones | `Sprite2D`, `AnimationPlayer`, `Control` |
| **Lógica de Juego** | Comportamiento de entidades | Scripts en `CharacterBody2D`, `Area2D` |
| **Sistemas Globales** | Estado global compartido | Autoloads (`GameManager`, `EventBus`, `SaveSystem`) |
| **Datos** | Configuración y estadísticas | Recursos `.tres`, `Resource` customizados |
| **Persistencia** | Guardado/carga | `FileAccess`, `ConfigFile` |

## Antipatrones Detectados en Discovery

1. **Rutas de nodo hardcodeadas**: `get_node("../../Player/Sprite2D")` — rompe al mover nodos.
2. **Scripts monolíticos**: Un solo `.gd` con física, UI, lógica de negocio y red mezclados.
3. **Estado global en variables de escena**: Variables del juego en nodos hijos en lugar de Autoloads o Resources.
