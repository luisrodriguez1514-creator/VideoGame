# Setup de Items y Herramientas (Blueprints)

Objetivo: crear Blueprints base para items recogibles, herramientas y recursos (tierra, arena, piedra, carbón, madera).

## 1) Estructuras de datos
- Crear un `Enum` **E_ItemType**: `Resource`, `Tool`, `Consumable`.
- Crear un `Enum` **E_ToolType**: `None`, `Axe`, `Pickaxe`, `Shovel`, `Sword`.

## 2) BP_ItemBase (Actor)
**Ruta sugerida:** `Content/Blueprints/Items/BP_ItemBase`

### Componentes
- StaticMesh (visual simple, puede ser placeholder)
- SphereCollision (pickup)

### Variables
- `ItemId` (Name)
- `DisplayName` (Text)
- `ItemType` (E_ItemType)
- `StackSize` (int)

### Eventos
- OnOverlap: añadir item al inventario (lógica futura), destruir actor

## 3) BP_ResourceItem (Child de BP_ItemBase)
**Ruta sugerida:** `Content/Blueprints/Items/BP_ResourceItem`

### Variables
- `ResourceType` (Name) -> `Dirt`, `Sand`, `Stone`, `Coal`, `Wood`

## 4) BP_ToolItem (Child de BP_ItemBase)
**Ruta sugerida:** `Content/Blueprints/Items/BP_ToolItem`

### Variables
- `ToolType` (E_ToolType)
- `Damage` (float)
- `Durability` (float)

## 5) Placeholders rápidos
Crear instancias:
- `BP_Item_Dirt` (ResourceItem)
- `BP_Item_Sand`
- `BP_Item_Stone`
- `BP_Item_Coal`
- `BP_Item_Wood`
- `BP_Tool_Axe`
- `BP_Tool_Pickaxe`
- `BP_Tool_Shovel`
- `BP_Tool_Sword`

## 6) Prueba rápida
1. Arrastra 2-3 items al mapa.
2. Play y verifica el overlap (por ahora destroy).
