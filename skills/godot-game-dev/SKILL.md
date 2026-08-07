---
name: godot-game-dev
description: Habilidad para diseñar y desarrollar videojuegos en Godot 4 (GDScript 2.0) integrando arquitectura de lore y narrativa viva.
---

# Skill: Godot Game Dev & Lore Integration

Esta habilidad guía al agente en la creación de videojuegos modulares en Godot 4 con tipado estático en GDScript, composición de nodos, patrones de EventBus y sincronización fluida con la arquitectura de historia documentada en `overview/lore/`.

## Principios Fundamentales

1. **Diseño Orientado a Nodos y Composición**:
   - Cada entidad de juego debe estar compuesta por nodos especializados (`CharacterBody2D/3D`, `CollisionShape`, `StateMachine`, `HealthComponent`, `AudioStreamPlayer`).
2. **Sincronización Lore ↔ Gameplay**:
   - Mapear el `overview/lore/narrative_tree.md` directamente a un Singleton de banderas (`StoryFlags.gd`) o un gestor de misiones (`QuestManager.gd`).
3. **Data-Driven con Recursos (`.tres`)**:
   - Definir estadísticas, items y diálogos en Recursos exportables.
4. **Clean GDScript 2.0**:
   - Tipado estático en variables, funciones y señales.
   - Scripts compactos (<250 líneas).
