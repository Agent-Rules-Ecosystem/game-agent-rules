# Adapter: Unity Engine

> Activar cuando el proyecto use **Unity 2022 LTS o superior**.  
> Complementa las reglas genéricas de `core/` con convenciones y patrones específicos de Unity.

---

## Identificación del proyecto

El agente debe activar este adapter si detecta cualquiera de:
- Carpeta `Assets/` con subcarpeta `ProjectSettings/` en la raíz.
- Archivo `*.unity` (escenas) o `*.prefab` en el proyecto.
- Archivo `Packages/manifest.json` (Unity Package Manager).

---

## Estructura de proyecto canónica

```
Assets/
  _Project/                ← contenido propio (evitar conflictos con paquetes)
    Scripts/
      Core/                ← sistemas base (GameManager, etc.)
      Entities/            ← lógica de entidades
      UI/                  ← controladores de UI (MonoBehaviour ligeros)
      Services/            ← servicios desacoplados (sin MonoBehaviour)
      Utils/               ← helpers y extensiones
    Prefabs/
      Entities/
      UI/
      FX/
    Scenes/
      Main.unity
      Game.unity
    ScriptableObjects/     ← datos de configuración (.asset)
    Shaders/
    Animations/
  Plugins/                 ← SDKs de terceros (no modificar)
Packages/
  manifest.json
ProjectSettings/
```

---

## Convenciones de código (C#)

### Nomenclatura

| Elemento | Convención | Ejemplo |
|---|---|---|
| Clase | `PascalCase` | `PlayerController` |
| Método público | `PascalCase` | `TakeDamage()` |
| Campo privado | `_camelCase` | `_healthPoints` |
| Propiedad | `PascalCase` | `HealthPoints` |
| Constante | `UPPER_SNAKE` | `MAX_SPEED` |
| Evento C# | `On + PascalCase` | `OnPlayerDied` |
| Interface | `I + PascalCase` | `IDamageable` |

### Límite de líneas por archivo

| Tipo | Límite |
|---|---|
| MonoBehaviour | ≤ 150L |
| ScriptableObject | ≤ 100L |
| Manager / Service | ≤ 200L |
| Utility / Extension | ≤ 80L |

---

## Patrones arquitectónicos

### ScriptableObject como datos (Data-Driven)

```csharp
// ✅ Correcto — datos desacoplados de lógica
[CreateAssetMenu(fileName = "EnemyData", menuName = "Game/Enemy Data")]
public class EnemyData : ScriptableObject
{
    public float MaxHealth;
    public float Speed;
}
```

### Eventos C# sobre FindObjectOfType

```csharp
// ✅ Correcto — sin acoplamiento
public static event Action<int> OnScoreChanged;

// ❌ Evitar — búsqueda costosa y acoplada
FindObjectOfType<UIManager>().UpdateScore(score);
```

### Services sin MonoBehaviour

Para lógica que no necesita ciclo de vida Unity:
```csharp
// ✅ Servicio puro — testeable
public class InventoryService : IInventoryService
{
    public void AddItem(ItemData item) { ... }
}
```

### GameManager como fachada

```
GameManager (MonoBehaviour, DontDestroyOnLoad)
  ├── GameStateService     — estado de partida
  ├── AudioService         — control de audio
  └── SaveService          — persistencia
```

---

## Comandos específicos de Unity

### `$archi` — extensiones Unity

En `overview/architecture/routes_map.md` documentar:
```markdown
## Scene Flow
- Main.unity → Bootstrap (carga inicial)
- Game.unity → gameplay principal
- UI.unity → (Additive) capa de UI persistente
```

En `overview/architecture/core/data_flow.md`:
- Listar todos los GameManagers con `DontDestroyOnLoad`
- Documentar eventos globales (`static event Action<T>`)
- Listar ScriptableObjects de configuración global

### `$close` — validación Unity

```bash
# Build headless de validación (si Unity CLI está disponible)
Unity -batchmode -projectPath . -executeMethod BuildScript.Build -quit -logFile build.log
```
Si Unity CLI no disponible → `validación: no aplica (CLI ausente)`.

---

## Anti-patrones específicos de Unity

| Anti-patrón | Problema | Solución |
|---|---|---|
| `FindObjectOfType<T>()` en Update | Muy costoso por frame | Cachear en `Awake()` o usar eventos |
| Lógica de negocio en MonoBehaviour | No testeable | Extraer a Services puros |
| Prefabs anidados sin Variants | Duplicación de datos | Usar Prefab Variants |
| `string` en `Animator.SetTrigger()` | Typos silenciosos | Usar hash: `Animator.StringToHash()` |
| `PlayerPrefs` para estado complejo | No escalable | Usar `ScriptableObject` + serialización JSON |
| `GetComponent<T>()` en Update | Overhead por frame | Cachear con `[SerializeField]` o `Awake()` |

---

## Assembly Definitions (asmdef)

Organizar el código en assemblies para reducir tiempo de compilación:

```
_Project/
  Scripts/
    Core/Core.asmdef
    Entities/Entities.asmdef    (depende de Core)
    UI/UI.asmdef                (depende de Core, Entities)
    Services/Services.asmdef   (depende de Core)
```

---

## Integración con el ecosistema

- **`$archi`**: genera `routes_map.md` con el Scene Flow y `data_flow.md` con el grafo de servicios.
- **`overview/learning.md`**: abstraer aprendizajes de Unity a reglas agnósticas antes de registrar.
- Las reglas de lore/narrativa del mundo del juego se gestionan con **Lore Skill** si está instalada.
