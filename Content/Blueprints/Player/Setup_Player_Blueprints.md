# Setup de Player (Blueprints)

Objetivo: crear los Blueprints base del personaje, controller y HUD para poder entrar al mundo, moverse y ver barras de vida/hambre/sed.

## 1) BP_PlayerCharacter (Character)
**Ruta sugerida:** `Content/Blueprints/Player/BP_PlayerCharacter`

### Componentes
1. **CapsuleComponent** (root)
2. **Mesh** (SkeletalMesh)
   - Asigna un esqueleto humano básico (UE5 Mannequin o equivalente).
3. **CameraBoom** (SpringArm)
   - TargetArmLength: 300
   - UsePawnControlRotation: true
4. **FollowCamera** (Camera)
   - Attach a CameraBoom
   - UsePawnControlRotation: false

### Variables
- `WalkSpeed` (float, default 350)
- `RunSpeed` (float, default 650)
- `CrouchSpeed` (float, default 200)
- `MaxHealth` (float, default 100)
- `Health` (float, default 100)
- `MaxHunger` (float, default 100)
- `Hunger` (float, default 100)
- `MaxThirst` (float, default 100)
- `Thirst` (float, default 100)
- `EquippedTool` (enum o name: `None/Axe/Pickaxe/Shovel/Sword`)

### Input (Enhanced Input recomendado)
- `Move` (Axis2D)
- `Look` (Axis2D)
- `Jump` (Action)
- `Sprint` (Action)
- `Crouch` (Action)
- `PrimaryAction` (Action) -> golpes/recolectar

### BeginPlay
- Set `Health = MaxHealth`, `Hunger = MaxHunger`, `Thirst = MaxThirst`
- Set `CharacterMovement.MaxWalkSpeed = WalkSpeed`

### Tick (lógica mínima de supervivencia)
- Reducir `Hunger` y `Thirst` lentamente (ej. 0.1/seg)
- Si `Hunger <= 0`: aplicar efecto de fatiga y daño gradual
- Si `Thirst <= 0`: aplicar efecto de insolación y daño gradual

> Nota: los efectos visuales pueden añadirse luego vía post-process o animación.

## 2) BP_PlayerController (PlayerController)
**Ruta sugerida:** `Content/Blueprints/Player/BP_PlayerController`

### Setup
- Asignar `Input Mapping Context` en BeginPlay
- Crear una referencia al HUD (widget) y agregarlo al viewport

## 3) BP_PlayerHUD (UserWidget)
**Ruta sugerida:** `Content/Blueprints/UI/WBP_PlayerHUD`

### Elementos UI
- Barra de Vida
- Barra de Hambre
- Barra de Sed
- Texto de Semilla (Seed)

### Binding
- En el widget, exponer un `PlayerRef` (BP_PlayerCharacter) y leer sus variables.

## 4) GameMode Base
**Ruta sugerida:** `Content/Blueprints/World/BP_GameMode`
- Default Pawn: `BP_PlayerCharacter`
- Player Controller: `BP_PlayerController`
- HUD Class: `WBP_PlayerHUD`

## 5) Prueba rápida
1. Crear un mapa `Maps/StarterMap`.
2. Colocar `BP_WorldManager` (del setup anterior).
3. En Project Settings → Maps & Modes, asignar `BP_GameMode`.
4. Play: mover personaje, saltar, ver HUD con barras.
