# Game Dev & Lore Agent Rules (Godot Engine)

Repositorio centralizado: cerebro operativo para desarrollo de juegos en Godot 4 (GDScript) y mapeo estructurado de historias, lore y sistemas narrativos.

## Qué aporta

1. **Mapeo Integrado de Lore y Narrativa (`overview/lore/`)**:
   - Árbol narrativo, actos, ramas de decisión y banderas de historia (`game_story_flags`).
   - Worldbuilding, cosmología, facciones, fichas de personajes y misiones.
   - Conexión directa entre nodos de diálogo y código GDScript / Recursos `.tres` de Godot.
2. **Estándar de Desarrollo en Godot 4 (GDScript 2.0)**:
   - Tipado estático obligatorio, patrón EventBus, composición de nodos ("Call down, Signal up") y máquinas de estado (FSM).
3. **Comunicación Concisa (Modo Cavernícola)** — Respuestas breves y ahorro de tokens.
4. **Memoria Versionada y Handoff de Agente**:
   - Sesión con firma de agente, historial de intentos firmado por fecha y modelo.
5. **$-Comandos**:
   - `$boot`, `$status`, `$close`, `$learn`, `$learnagnostico`, `$work` para operar de forma inmediata.

## Instalación en tu Proyecto de Juego

### 1. Core (`.agents`)
```bash
git submodule add git@github.com:xolotl-hub/game-agent-rules.git .agents
```

### 2. Instalación de Skills (`.skill/` en la raíz)

```bash
git submodule add git@github.com:Agent-Rules-Ecosystem/lore-agent-skill.git .skill/lore-agent-skill
git submodule add git@github.com:Agent-Rules-Ecosystem/second-brain-agent-rules.git .skill/second-brain-agent-skill
```

Instalar el adaptador de `.agents/adapters/` adecuado para tu entorno (Claude, Gemini, Cursor). En tu proyecto de juego, inicializar `overview/` desde `.agents/templates/` (o escribir `$boot`).

## Estructura de Lore (`overview/lore/`)

```
overview/lore/
├── narrative_tree.md    # Árbol narrativo y banderas de decisión
├── worldbuilding.md     # Universo, eras, geografía y leyes
├── characters.md        # Fichas de personajes y arcos
├── quests.md            # Misiones principales y secundarias
├── dialogues.md         # Nodos de conversación
└── factions.md          # Facciones y diplomacia
```

## Uso Rápido de Comandos

| Escribir | Resultado |
|---|---|
| `$boot` | Bootstrap completo del juego + mapeo de Godot y Lore |
| `$status` | Resumen del estado actual técnico y narrativo |
| `$archi` | Actualiza mapa técnico de Godot en `overview/architecture.md` (Hub) y `overview/architecture/` (Spoke) |
| `$close` | Cierre de sesión y verificación de GDScript / Lore |
| `$learn [texto]` | Registrar aprendizaje candidato del core |
| `$learnagnostico [texto]` | Abstraer y registrar regla genérica de juego/lore |
| `$work [descripción]` | Registrar nueva tarea, bug o nodo de lore |
| `ejecuta .agents` | Bootstrap completo + auditoría de aprendizajes |
