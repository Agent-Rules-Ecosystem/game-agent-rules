# Adapter: Unreal Engine

> Activar cuando el proyecto use **Unreal Engine 5.x**.  
> Complementa las reglas genéricas de `core/` con convenciones y patrones específicos de UE5.

---

## Identificación del proyecto

El agente debe activar este adapter si detecta cualquiera de:
- Archivo `*.uproject` en la raíz del proyecto.
- Carpeta `Content/` con archivos `.uasset` o `.umap`.
- Carpeta `Source/` con archivos `Build.cs` o `Target.cs`.

---

## Estructura de proyecto canónica

```
MyGame/
  Content/                    ← assets del juego (UE Asset Manager)
    Characters/
    Environments/
    UI/                       ← Widgets UMG (.uasset)
    VFX/
    Audio/
    Maps/                     ← niveles (.umap)
    Blueprints/               ← BPs de alto nivel / prototipos
  Source/
    MyGame/                   ← módulo principal C++
      Public/                 ← headers (.h)
        Actors/
        Components/
        GameModes/
        Interfaces/
        UI/
      Private/                ← implementaciones (.cpp)
        Actors/
        Components/
        ...
      MyGame.Build.cs
    MyGameEditor/             ← módulo editor-only (opcional)
  Config/
    DefaultGame.ini
    DefaultEngine.ini
    DefaultInput.ini
  MyGame.uproject
```

---

## Convenciones de código (C++ / Blueprints)

### Prefijos de clase UE5

| Tipo | Prefijo | Ejemplo |
|---|---|---|
| Actor | `A` | `APlayerCharacter` |
| UObject / Component | `U` | `UHealthComponent` |
| Struct | `F` | `FInventoryItem` |
| Interface | `I` | `IDamageable` |
| Enum | `E` | `EGameState` |
| Blueprint | `BP_` | `BP_Enemy` |
| Widget UMG | `WBP_` | `WBP_HUD` |

### Nomenclatura

| Elemento | Convención | Ejemplo |
|---|---|---|
| Función pública | `PascalCase` | `TakeDamage()` |
| Variable miembro | `PascalCase` (sin prefijo) | `HealthPoints` |
| Variable local | `camelCase` | `healthPoints` |
| Macro UPROPERTY | `PascalCase` | `MaxHealth` |
| Delegate | `F + Nombre + Delegate` | `FOnPlayerDiedDelegate` |

### Límite de líneas por archivo

| Tipo | Límite |
|---|---|
| Actor header (.h) | ≤ 100L |
| Actor implementation (.cpp) | ≤ 200L |
| Component (.h + .cpp) | ≤ 150L combinado |
| GameMode / GameState | ≤ 150L |

---

## Patrones arquitectónicos

### C++ para lógica, Blueprint para datos

```
// ✅ Patrón correcto
// C++: lógica base, expuesta a Blueprint
UFUNCTION(BlueprintImplementableEvent)
void OnHealthChanged(float NewHealth);

// Blueprint: implementa la parte visual/artística
// BP_PlayerCharacter hereda de APlayerCharacter (C++)
```

### Gameplay Ability System (GAS) — para juegos complejos

```
Actor
  └── AbilitySystemComponent (UAbilitySystemComponent)
        ├── GameplayAbilities   ← habilidades
        ├── GameplayEffects     ← modificadores de atributos
        └── AttributeSet        ← stats del personaje
```

### Delegates sobre referencias directas

```cpp
// ✅ Correcto — desacoplado
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnPlayerDied, APlayerCharacter*, Player);
UPROPERTY(BlueprintAssignable)
FOnPlayerDied OnPlayerDied;

// ❌ Evitar — referencia directa entre actores
Cast<AUIManager>(GetWorld()->GetFirstPlayerController())->ShowDeathScreen();
```

### GameMode / GameState / PlayerState

```
GameMode (server-only)          ← reglas del juego
GameState (replicado)           ← estado global visible por todos
PlayerState (por jugador)       ← stats por jugador (replicado)
PlayerController                ← input y lógica de jugador
Pawn / Character                ← representación física
```

---

## Comandos específicos de Unreal

### `$archi` — extensiones UE5

En `overview/architecture/routes_map.md` documentar:
```markdown
## Level Flow
- MainMenu.umap → menú principal
- Game_01.umap → nivel 1 (persistent + streaming sublevels)
- GameMode: ABP_GameMode → controla flujo de partida
```

En `overview/architecture/core/data_flow.md`:
- Documentar GameMode y GameState activos
- Listar Subsystems registrados (UGameInstanceSubsystem)
- Listar DataAssets de configuración global

### `$close` — validación UE5

```bash
# Build en modo Development desde CLI (si UE está en PATH)
UnrealBuildTool MyGame Win64 Development -Project="MyGame.uproject"
```
Si UBT no disponible → `validación: no aplica (CLI ausente)`.

---

## Anti-patrones específicos de UE5

| Anti-patrón | Problema | Solución |
|---|---|---|
| `Cast<T>()` en Tick | Muy costoso por frame | Cachear el resultado en `BeginPlay()` |
| Toda la lógica en Blueprint | No escalable, difícil de versionar | C++ para lógica, BP para datos/visuales |
| `GetAllActorsOfClass()` en Tick | O(n) scan del mundo cada frame | Usar referencias directas o delegates |
| Blueprints con +100 nodos | Ilegible, no debuggeable | Refactorizar a C++ o dividir en funciones |
| Hard references en `UPROPERTY` | Carga todos los assets al inicio | Usar `TSoftObjectPtr<T>` + Async Load |
| Lógica de gameplay en Widget UMG | Acoplamiento Vista-Lógica | Delegar a PlayerController o GameMode |

---

## Módulos y Build.cs

Separar código en módulos para compilación incremental:

```csharp
// MyGame.Build.cs
PublicDependencyModuleNames.AddRange(new string[] {
    "Core", "CoreUObject", "Engine",
    "InputCore", "EnhancedInput",
    "GameplayAbilities", "GameplayTags"  // si usas GAS
});
```

---

## Integración con el ecosistema

- **`$archi`**: genera `routes_map.md` con Level Flow y GameMode chain, `data_flow.md` con Subsystems y replicación.
- **`overview/learning.md`**: abstraer aprendizajes de UE5 a reglas agnósticas antes de registrar.
- Las reglas de lore/narrativa se gestionan con **Lore Skill** si está instalada.
