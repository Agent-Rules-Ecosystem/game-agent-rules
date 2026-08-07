<<<<<<< HEAD
# Game Dev & Lore Agent Rules adapter
=======
# Flutter Agent Rules — Codex Adapter
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

> Codex (OpenAI) lee este archivo automáticamente como `AGENTS.md`.
> Las reglas viven en `.agents/`; **no duplicar aquí**.

## Qué hacer al iniciar

1. Leer `.agents/AGENTS.md` completo antes de responder o editar.
2. Si no existe `overview/` en la raíz del proyecto → crearla desde `.agents/templates/`.
3. Cargar: `overview/session.md`, `overview/work.md`, `overview/work/tasks.md`.
4. Si el agente anterior fue distinto → activar protocolo Handoff (`core/brain.md §Handoff`).

## Qué hacer al trabajar

- Actualizar `overview/work.md` y `overview/work/tasks.md` **antes** de editar código.
- Cambios quirúrgicos: no mejorar código ajeno sin necesidad.
- Referencias rápidas: `$boot` `$status` `$close` `$learn` `$work` (ver `.agents/core/commands.md`).

## Qué hacer al cerrar

1. Actualizar `overview/session.md` con firma: `[Modelo] — YYYY-MM-DD`.
2. Registrar pendientes en `overview/work/pendientes.md`.
3. Indicar validación: `verificado` | `no verificado` | `no aplica`.

> Estado del proyecto → `overview/`. Reglas globales → `.agents/`. No duplicar.
