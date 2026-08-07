# Comandos del Core ($-commands)

Cuando el usuario escribe un comando con prefijo `$`, el agente lo reconoce como instrucción explícita y ejecuta el protocolo correspondiente **inmediatamente**, sin esperar bootstrap automático.

> Propósito: compensar los casos donde el bootstrap automático fue incompleto o no se disparó.

---

## Referencia rápida

| Comando | Acción |
|---|---|
| `$boot` | Bootstrap completo del proyecto |
| `$status` | Mostrar estado actual en resumen |
| `$close` | Protocolo de cierre de sesión |
| `$learn [texto]` | Registrar aprendizaje candidato |
| `$learnagnostico [texto]` | Abstraer a términos genéricos y registrar |
| `$work [descripción]` | Registrar nueva tarea/bug |

---

## Definición de cada comando

### `$boot`

Dispara el bootstrap completo. Equivalente a **"ejecuta .agents"** pero más corto.

Pasos que el agente debe ejecutar:
1. Leer `core/path_map.md`, `core/communication.md`, `core/brain.md`, `core/commands.md`.
2. Verificar si existe `overview/` — si no, crear desde `templates/`.
3. Cargar `overview/session.md`, `overview/work.md`, `overview/work/tasks.md`, `overview/work/deuda_tecnica.md`, `overview/work/pendientes.md`, `overview/trackers/progress.md`.
4. Detectar si el `Agente:` en `session.md` difiere del modelo actual → si difiere, activar protocolo `## Handoff de Agente` de `brain.md`.
5. Alias divergentes: si alias y canónico coexisten con contenido distinto (`tasks.md`/`work.md`, `tracker.md`/`trackers/architecture.md`) → flag `[consolidar alias]` en `work.md`.
6. `session.md` legado: si faltan `Agente:`, `## Reanudar` o `## Cambios` → reportar `session legado` (sin migrar automático).
7. Auditoría de líneas: listar archivos de código fuente >250L; sugerir IDs `deuda` en `overview/work/deuda_tecnica.md` (prioridades **Alta**, **Media**, **Baja**).
8. Auditar `overview/learning.md` (Evaluación de 3 Vías): promover aplicadas al Histórico, eliminar/marcar rechazadas y flag `[conflicto learning]` si hay choque con el Core.
9. **Revisión de Trabajo (`work_review.md`)**: Ejecutar el protocolo de revisión de `overview/work/` respetando prioridades (1º `tasks.md`, 2º `pendientes.md`, 3º `deuda_tecnica.md`) según `templates/work_review.md`.
10. Reportar en 5 líneas máximo: agente anterior, nodo activo, tareas pendientes, estado validación, flags (alias/session/líneas/conflicto), síntesis de `work_review` y próximo paso.

---

### `$status`

Mostrar el estado actual del proyecto sin modificar ningún archivo.

El agente debe leer y reportar en formato compacto:
```
Agente activo : [firma]
Nodo activo   : [id de progress.md]
Validación    : [verificado | no verificado | no aplica]
Tareas abiertas: [IDs y resumen de work.md con estado ≠ hecho]
Próximo paso  : [## Reanudar de session.md]
```

---

### `$close`

Protocolo de cierre de sesión. El agente debe:
<<<<<<< HEAD
1. Validar sintaxis GDScript o estado de escenas cuando aplique.
2. Actualizar `overview/work.md` con cambios de gameplay/lore de la sesión.
3. Actualizar `overview/session.md`:
   - Registrar `Agente:` con firma propia.
   - Completar `## Cambios` con lo trabajado en código o historia.
   - Completar `## Reanudar` con el siguiente nodo/misión y contexto crítico.
4. Actualizar `overview/trackers/progress.md` y archivos de `overview/lore/` modificados.
5. Si hay sesiones antiguas irrelevantes → archivar en `overview/history/`.
6. Si hay mejora candidata identificada → agregar a `overview/learning.md`.
7. Reportar: `Sesión cerrada. Próximo: [nodo/misión]. Estado: [verificado/no verificado/no aplica].`
=======
1. Ejecutar `flutter analyze` si aplica. Suite de tests: ausente (sin carpeta `test/`) → `no aplica`; presente y no corrida/fallida → `no verificado` + motivo. Si la tarea implica build o release → consultar `.agents/knowledge/release_checklist.md`.
2. Registrar ítems o tareas secundarias identificadas durante la ejecución en `overview/work/pendientes.md`.
3. Actualizar índice maestro `overview/work.md` con cambios de la sesión y trasladar ítems/deudas resueltas a `## ✅ Completados (Historial)` conservando su ID.
4. Actualizar `overview/session.md`:
   - Registrar `Agente:` con firma propia.
   - Completar `## Cambios` con lo trabajado.
   - Completar `## Reanudar` con el siguiente nodo y contexto crítico.
5. Actualizar `overview/trackers/progress.md`.
6. Si hay sesiones antiguas irrelevantes → archivar en `overview/history/`.
7. Si hay mejora candidata identificada → agregar a `overview/learning.md`.
8. Reportar: `Sesión cerrada. Próximo: [nodo]. Estado: [verificado/no verificado/no aplica].`
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

---

### `$learn [texto]`

Registrar un aprendizaje candidato en `overview/learning.md`.

El agente debe:
1. Validar el texto con el **Filtro Agnóstico** (`brain.md`): rechazar código específico, snippets de UI o comandos CLI rígidos. Si contiene código o comandos, abstraer a regla o proceso de diagnóstico agnóstico.
2. Abrir `overview/learning.md`.
3. Agregar bajo `## 📌 Propuestas de mejora` un bullet con el texto agnóstico.
4. Si el archivo no existe, crearlo desde `templates/learning.md`.
5. Confirmar: `Aprendizaje registrado en overview/learning.md.`

Ejemplo de uso:
```
$learn Usar EventBus Autoload para desacoplar emisiones de daño entre personajes y UI en Godot
```

---

### `$learnagnostico [texto]`

Abstraer un aprendizaje candidato descontextualizando el proyecto antes de registrar.

El agente debe:
<<<<<<< HEAD
1. Sustituir nombres propios de juego/personajes/rutas por términos genéricos de arquitectura (entidad, FSM, inventario, nodo narrativo, quest manager, etc.).
2. Eliminar IDs de misiones, personajes concretos y paths de proyecto.
=======
1. Sustituir nombres propios de app/módulo/ruta y términos específicos de negocio (ej. joyas, mascotas, inventarios) por términos genéricos de arquitectura agnósticos (entidad, procesamiento, capa, destino, persistencia, navegación, etc.).
2. Eliminar IDs de negocio, pantallas concretas y paths de proyecto.
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17
3. Aplicar **Filtro Agnóstico** (`brain.md`) al texto resultante.
4. Registrar el bullet abstraído en `overview/learning.md` bajo `## 📌 Propuestas de mejora` (crear desde plantilla si falta).
5. Confirmar: `Aprendizaje agnóstico registrado.` + mostrar una línea con el texto final.

Ejemplo:
```
<<<<<<< HEAD
$learnagnostico En Eldoria la bandera de decisión Acto1_AliadoBosque debe sincronizarse con el QuestResource
```
→ bullet: `Sincronizar banderas de decisiones narrativas con los recursos (.tres) de misiones a través de un Singleton de estado.`
=======
$learnagnostico En MóduloX el flujo Entrada→Inventario→Salida debe documentarse aparte de architecture
```
→ bullet: `Documentar flujos de dominio (origen → procesamiento → destino) en overview/workflows/, no en architecture.md.`
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

---

### `$work [descripción]`

<<<<<<< HEAD
Registrar una nueva tarea, bug o nodo de lore en `overview/work.md`.
=======
Registrar una nueva tarea o bug en el sistema de trabajo modular `overview/work/`.
>>>>>>> d55316b03e7586d1fbcfb117550721f2b8c07a17

El agente debe:
1. Determinar tipo: `tarea` (feature/gameplay), `lore` (diseño de historia/misiones/dialogos), `bug` (comportamiento inesperado) o `deuda`.
2. Generar el próximo ID correlativo (ej. `w4` si el último es `w3`).
3. Registrar en `overview/work/tasks.md`: indicar la tarea a iniciar, clasificarla (`problema`, `mejora`, `refactor`) y redactar hipótesis/soluciones planteadas.
4. Agregar fila en el índice maestro `overview/work.md` con el ID, tipo y estado `pendiente`.
5. **Mapeo incremental de arquitectura**: Actualizar `overview/architecture.md` **únicamente con los nodos** (pantallas, clases, providers, repos) que la tarea concretamente va a tocar (sin sweep completo del repo).
6. Si es un bug: agregar entrada vacía en `## 📋 Historial de Intentos` en `work.md` con header `### [ID] [descripción]`.
7. Confirmar: `Registrado como [ID] en work.md, mapeado en architecture.md y configurado en overview/work/tasks.md.`

Ejemplo de uso:
```
$work lore: Diseñar arbol de dialogo para el guardián de las ruinas en Acto 2
```
```
$work bug: El CharacterBody2D atraviesa la colisión al realizar el dash
```


---

## Reglas de parsing

- El prefijo `$` debe ser el **primer carácter** del mensaje o estar en línea propia para ser reconocido como comando.
- Si el `$`-comando va acompañado de texto adicional (ej. `$learn texto aquí`), el texto después del comando es el argumento.
- Si el argumento falta donde es requerido, el agente debe pedirlo en una sola línea.
- Los comandos son **case-insensitive**: `$Boot`, `$BOOT` y `$boot` son equivalentes.
- Si el agente no reconoce el comando, responder: `Comando desconocido. Disponibles: $boot $status $close $learn $learnagnostico $work`.
