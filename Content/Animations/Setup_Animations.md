# Setup de Animaciones

Objetivo: preparar el flujo mínimo para animaciones del personaje: caminar, correr, saltar, agacharse, golpear y usar herramientas.

## 1) Skeleton y AnimBP
- Importar el esqueleto humano base (UE5 Mannequin o equivalente).
- Crear `ABP_Player` (Animation Blueprint) asociado al esqueleto.

## 2) Animaciones necesarias (placeholders)
- Idle
- Walk
- Run
- JumpStart / JumpLoop / JumpEnd
- CrouchIdle / CrouchWalk
- Attack_Base (golpe genérico)
- Attack_Axe
- Attack_Pickaxe
- Attack_Shovel
- Attack_Sword

## 3) Blend Space
- Crear `BS_WalkRun` con velocidad 0-600.

## 4) State Machine sugerida
**Locomotion**
- Idle/Walk/Run (blend space)
- Jump
- Crouch

**Combat/Tool Use** (Slot + montajes)
- Usar AnimMontage para cada ataque/herramienta.

## 5) Eventos Notifies
- Agregar notify `HitWindow` en cada ataque para disparar daño o recolección.

## 6) Conectar al BP_PlayerCharacter
- En `BP_PlayerCharacter`, asignar `ABP_Player` a la SkeletalMesh.
- Al usar herramienta, reproducir el montage correspondiente.
