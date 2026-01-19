# Setup de Data: Items

Objetivo: crear DataTables para definir recursos y herramientas.

## 1) Struct
Crear un `Struct` **S_ItemData** con:
- `ItemId` (Name)
- `DisplayName` (Text)
- `ItemType` (E_ItemType)
- `ToolType` (E_ToolType)
- `Damage` (float)
- `MaxStack` (int)

## 2) DataTable
**Ruta sugerida:** `Content/Data/Items/DT_Items`

### Filas sugeridas
- `Dirt`: Resource
- `Sand`: Resource
- `Stone`: Resource
- `Coal`: Resource
- `Wood`: Resource
- `Axe`: Tool (Damage 10)
- `Pickaxe`: Tool (Damage 12)
- `Shovel`: Tool (Damage 6)
- `Sword`: Tool (Damage 15)
