# Arquitectura de Juego (Godot Engine)

Mapa vivo de escenas, autoloads, nodos y sistemas del juego en Godot 4.

```mermaid
graph TD
    Main[Main / SceneManager] --> Level[Escena de Nivel / Level.tscn]
    Main --> UI[HUD / Menús]
    Level --> Player[Jugador / Player.tscn]
    Level --> Enemies[Enemigos / NPCs]
    Level --> Environment[Mapas / TileMaps / Environment]
    Player --> FSM[State Machine]
    Player --> Stats[StatsResource (.tres)]
    UI --> EventBus[EventBus Autoload]
    Player --> EventBus
    EventBus --> StoryFlags[StoryFlags Autoload]
```

## Nodos y Escenas Clave

| Categoría | Ruta de Escena / Script | Propósito / Responsabilidad |
|---|---|---|
| Autoload (Singleton) | `res://autoload/event_bus.gd` | Bus de señales globales (Gameplay ↔ UI) |
| Autoload (Singleton) | `res://autoload/story_flags.gd` | Registro de banderas de historia y progreso de lore |
| Autoload (Singleton) | `res://autoload/audio_manager.gd` | Gestor de música de fondo y efectos de sonido |
| Escena Principal | `res://scenes/main/main.tscn` | Carga de niveles, transiciones de pantalla y pausado |
| Entidad Jugador | `res://scenes/entities/player/player.tscn` | Movimiento, colisiones y control del jugador |
| Interfaz (UI) | `res://scenes/ui/hud/hud.tscn` | Barra de vida, inventario y texto de misiones |

## Sistemas y Recursos (.tres)

| Sistema | Tipo / Ruta | Descripción |
|---|---|---|
| Máquina de Estados (FSM) | `res://scripts/components/state_machine.gd` | Manejo de estados (Idle, Run, Attack, Dialogue) |
| Recursos de Estadísticas | `res://resources/stats/` | Definen vida, daño y velocidad de entidades |
| Gestor de Misiones | `res://scripts/systems/quest_manager.gd` | Carga y verifica misiones desde `overview/lore/quests.md` |
