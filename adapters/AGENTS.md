# Game Agent Rules — Adapters

> Este directorio contiene los adapters por motor de juego.  
> El agente debe activar el adapter correspondiente al detectar el motor del proyecto.

## Adapters disponibles

| Archivo | Motor | Activar cuando detectes |
|---|---|---|
| `godot.md` | Godot 4.x | `project.godot`, archivos `.gd` / `.tscn` |
| `unity.md` | Unity 2022+ | carpeta `Assets/` + `Packages/manifest.json` |
| `unreal.md` | Unreal Engine 5 | archivo `*.uproject`, carpeta `Source/` con `Build.cs` |

## Cómo activar un adapter

Al hacer `$boot`, después de cargar `core/`, el agente debe:

1. Escanear la raíz del proyecto de juego en busca de los indicadores de la tabla anterior.
2. Leer el adapter correspondiente (`adapters/godot.md`, `adapters/unity.md` o `adapters/unreal.md`).
3. Combinar las reglas del adapter con las reglas base de `core/`.
4. Si se detectan **dos o más motores** → preguntar al usuario cuál es el motor principal.

## Reglas comunes a todos los adapters

- Límite de líneas por archivo de código: ver tabla en cada adapter.
- Señales/Eventos/Delegates preferidos sobre referencias directas.
- Estado global mínimo: solo lo verdaderamente compartido entre todos los sistemas.
- `$archi` siempre genera `routes_map.md` con el flujo de escenas del motor activo.

> Reglas base del core → `.agents/core/`. Estado del proyecto → `overview/`. No duplicar aquí.
