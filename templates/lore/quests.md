# Misiones y Quests

Tracker maestro de misiones principales, secundarias y misiones de facción.

## Misiones Principales (Main Quests)

### `mq_001`: [Nombre de la Misión Principal 1]
- **Acto**: Acto 1
- **Detonante (Trigger)**: Hablar con NPC [Nombre] tras completar el tutorial.
- **Requisitos**: `flag: act1_started == true`
- **Objetivos**:
  1. [ ] Explorar las ruinas olvidadas.
  2. [ ] Recuperar el fragmento de cristal.
  3. [ ] Escapar antes de que colapse la cueva.
- **Decisiones / Bifurcaciones**:
  - Opción A: Entregar el cristal al Gremio (`set_flag: crystal_given_guild = true`).
  - Opción B: Conservar el cristal (`set_flag: crystal_kept_player = true`).
- **Recompensas**: 500 XP, Artefacto de Cristal, +10 reputación Gremio.
- **Recurso Godot**: `res://resources/quests/mq_001.tres`

---

## Misiones Secundarias (Side Quests)

### `sq_001`: [Nombre de la Misión Secundaria 1]
- **Región**: [Nombre de la zona]
- **NPC Emisor**: [Nombre de NPC]
- **Objetivo**: Recolectar 5 plantas curativas en el bosque.
- **Recompensa**: Poción de Vida x3, 100 Monedas.
- **Recurso Godot**: `res://resources/quests/sq_001.tres`
