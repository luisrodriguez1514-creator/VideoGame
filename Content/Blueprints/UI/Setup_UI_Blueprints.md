# Setup de UI (Blueprints)

Objetivo: crear widgets básicos para HUD, inventario y mensajes de estado.

## 1) WBP_PlayerHUD
**Ruta sugerida:** `Content/Blueprints/UI/WBP_PlayerHUD`

### Elementos
- ProgressBar `PB_Health`
- ProgressBar `PB_Hunger`
- ProgressBar `PB_Thirst`
- TextBlock `TXT_Seed`

### Variables
- `PlayerRef` (BP_PlayerCharacter, Expose on Spawn)

### Bindings
- `PB_Health.Percent` -> `PlayerRef.Health / PlayerRef.MaxHealth`
- `PB_Hunger.Percent` -> `PlayerRef.Hunger / PlayerRef.MaxHunger`
- `PB_Thirst.Percent` -> `PlayerRef.Thirst / PlayerRef.MaxThirst`
- `TXT_Seed` -> obtener semilla desde `BP_WorldManager`

## 2) WBP_Inventory (placeholder)
**Ruta sugerida:** `Content/Blueprints/UI/WBP_Inventory`

### Elementos
- Panel con slots (GridPanel o UniformGrid)
- Texto “Inventario (placeholder)”

## 3) WBP_StatusMessage (placeholder)
**Ruta sugerida:** `Content/Blueprints/UI/WBP_StatusMessage`

### Uso
- Mensajes temporales: “Tienes hambre”, “Tienes sed”.

## 4) Prueba rápida
1. Abrir `BP_PlayerController`.
2. En BeginPlay, crear `WBP_PlayerHUD` con `PlayerRef`.
3. Add to Viewport.
