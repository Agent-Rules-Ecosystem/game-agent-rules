# Nodos de Diálogo y Conversaciones

Diseño de árboles de diálogo y eventos narrativos conectables con Godot (Dialogue Manager / Dialogic / Custom Resource).

## Estructura de Nodo de Diálogo

```mermaid
graph TD
    NodeStart[Nodo start_npc_guard] --> Text1["Guardia: '¡Alto! Nadie cruza el puente sin permiso.'"]
    Text1 --> Choice1{"Respuestas del Jugador"}
    Choice1 -- Opción 1: Mostrar Pase --> NodePase["Guardia: 'Todo en orden, puedes pasar.' -> Set flag: bridge_unlocked"]
    Choice1 -- Opción 2: Sobornar (50 oros) --> CheckGold{"¿Tiene 50 oros?"}
    Choice1 -- Opción 3: Atacar --> NodeCombat["Iniciar Combate -> Trigger Event: start_battle_guard"]
    CheckGold -- Sí --> NodeSoborno["Guardia: 'No vi nada...' -> Restar 50 oros"]
    CheckGold -- No --> NodeSinOro["Guardia: '¿Intentas burlarte de mí?'"]
```

## Nodos de Diálogo Especificados

### Conversación: `dlg_npc_guard_bridge`
- **Locutor**: Guardia del Puente (`npc_guard_01`)
- **Condición de Entrada**: `flag: bridge_unlocked == false`

#### Nodo `start`:
- **Texto**: *"¡Alto! Nadie cruza las puertas del valle sin la autorización del Comandante."*
- **Opciones**:
  1. `[Mostrar documento]` (Requiere item: `item_pass_valley`) -> Saltar a `node_pass_accepted`
  2. `[Intimidar]` (Comprobación Fuerza >= 12) -> Saltar a `node_intimidate_success` / `node_intimidate_fail`
  3. *"Regresaré más tarde."* -> Cerrar diálogo.

#### Eventos de Salida (GDScript Signal Callbacks):
- `node_pass_accepted`: `EventBus.emit_signal("flag_changed", "bridge_unlocked", true)`
- `node_intimidate_fail`: `EventBus.emit_signal("start_combat", "npc_guard_01")`
