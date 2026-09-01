# Checklist pre-release Game (Godot / Unity / Unreal)

Cuando el usuario pida exportar o generar build ejecutable del juego: ejecutar checklist, mostrar comandos; no exportar sin solicitud explícita.

- [ ] Linter y verificación de scripts (GDScript / C# / C++) sin errores nuevos.
- [ ] Suite de pruebas verde (ej. Gut test runner para Godot, NUnit para Unity), si existen tests.
- [ ] Sin `print()` / `GD.Print()` de debug olvidados en scripts de producción.
- [ ] Configuración de Input Map y recursos exportables auditada (`export_presets.cfg` / `ProjectSettings`).
- [ ] `overview/trackers/progress.md` y tracker correspondiente actualizados.

## Exportación Godot CLI

```bash
godot --headless --export-release "Linux/X11" build/game.x86_64
```
