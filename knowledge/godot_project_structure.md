# Estructura Estándar de Proyecto Godot 4

Especifica las carpetas y archivos nativos estándar reconocidos en un proyecto Godot 4. Durante el protocolo de discovery, cualquier carpeta raíz fuera de esta lista es **no-estándar** y debe procesarse mediante inspección semántica.

## Directorios Estándar de Godot 4

| Directorio | Propósito | Tratamiento |
|---|---|---|
| `scenes/` | Escenas `.tscn` y sus recursos asociados | Conservar en root |
| `scripts/` | Scripts GDScript `.gd` y C# `.cs` | Conservar en root |
| `assets/` o `art/` | Sprites, modelos 3D, sonidos, fuentes | Conservar en root |
| `addons/` | Plugins de Godot instalados | Conservar en root |
| `autoloads/` o `globals/` | Singletons/Autoloads del proyecto | Conservar en root |
| `resources/` | Recursos `.tres` y `.res` de dominio | Conservar en root |
| `ui/` o `hud/` | Escenas de UI e HUD | Conservar en root |
| `docs/lore/` | Documentación narrativa del juego | Conservar en root |
| `.godot/` | Cache de Godot (ignorar en discovery) | Ignorar |
| `.agents/` | Submódulo oficial de reglas compartidas | Conservar en root |
| `overview/` | Estado local versionado del proyecto | Conservar en root |

## Archivos Estándar en Root

- `project.godot` — Configuración principal del proyecto
- `export_presets.cfg` — Configuración de exportación por plataforma
- `.gitignore`, `.gitattributes`
- `README.md`, `LICENSE`

## Regla de Inspección para Carpetas No-Estándar

Cualquier otro directorio en root debe inspeccionarse recursivamente y clasificarse según `core/brain.md`.
