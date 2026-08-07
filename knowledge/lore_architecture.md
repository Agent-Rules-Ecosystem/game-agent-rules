# Arquitectura de Lore y Narrativa de Juego

Este documento define la metodología para mapear y estructurar la historia, cosmología, personajes, misiones y diálogos de un videojuego en el directorio `overview/lore/`, garantizando su perfecta integración con el código GDScript en Godot.

## Estructura del Mapeo de Lore (`overview/lore/`)

```
overview/lore/
├── narrative_tree.md    # Árbol de decisiones, actos, capítulos y banderas narrativas
├── worldbuilding.md     # Cosmología, historia del mundo, regiones, magia/tecnología
├── characters.md        # Fichas de personajes, arcos de evolución, motivaciones
├── quests.md            # Misiones principales/secundarias, detonantes y recompensas
├── dialogues.md         # Nodos de conversación y conexiones con el juego
└── factions.md          # Facciones, matriz de alineamiento y relaciones socio-políticas
```

## Componentes del Mapeo Narrativo

### 1. Árbol Narrativo (`narrative_tree.md`)
- **Actos y Capítulos**: División temporal y dramática de la historia.
- **Nodos de Decisiones (Decision Nodes)**: Elecciones críticas del jugador y sus consecuencias.
- **Banderas de Historia (`game_story_flags`)**: Variables booleanas o de entero que rastrean decisiones (ej. `Act1_SparedBoss = true`).
- **Ramas y Finales (Branching & Endings)**: Matriz de condiciones que desbloquean finales o rutas alternativas.

### 2. Worldbuilding (`worldbuilding.md`)
- **Línea de Tiempo Histórica**: Eras pasadas, eventos cataclísmicos y época actual.
- **Regiones y Geografía**: Clima, cultura, lugares clave y peligros.
- **Sistemas de Reglas (Magia / Ciencia)**: Límites y normas del mundo que el gameplay debe respetar.

### 3. Fichas de Personajes (`characters.md`)
- **Atributos Narrativos**: Nombre, bando/facción, rol en la historia, secreto/conflicto interno.
- **Voz y Diálogo**: Tono de voz, muletillas, actitud hacia el protagonista.
- **Conexiones con Gameplay**: Escena Godot asociada (`scenes/characters/npc_guard.tscn`), Stats Resource (`resources/stats/npc_guard_stats.tres`).

### 4. Misiones (`quests.md`)
- **Estados de Misión**: `no_iniciada` -> `activa` -> `objetivo_cumplido` -> `completada` / `fallida`.
- **Condiciones de Inicio y Fin**: Banderas narrativas o ítems requeridos.
- **Recompensas**: Experiencia, ítems, cambios en el favor de facciones.

### 5. Árboles de Diálogo (`dialogues.md`)
- **Estructura de Nodos de Conversación**: ID de nodo, locutor, texto, opciones de respuesta, condiciones de desbloqueo y eventos GDScript resultantes.

## Conexión Lore ↔ Godot GDScript

Para que el mapa de lore cobre vida en Godot:

1. **StoryFlags Singleton (`autoload/story_flags.gd`)**:
   - Mantiene un diccionario de banderas narrativas cargadas desde las decisiones documentadas en `narrative_tree.md`.
2. **QuestResources (`.tres`)**:
   - Cada misión definida en `quests.md` se traduce en un recurso de Godot con export variables tipadas.
3. **Integración con Dialogue Manager / Dialogic**:
   - Los nodos de diálogo de `dialogues.md` alimentan los archivos de diálogo del plugin o sistema personalizado de Godot.
