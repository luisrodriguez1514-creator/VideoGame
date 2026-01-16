# Setup de Materiales

Objetivo: crear materiales base para voxel realista (tierra, arena, piedra, carbón, madera).

## 1) Material Master
**Ruta sugerida:** `Content/Materials/M_Master_Voxel`

### Parámetros
- BaseColor (Vector)
- Roughness (Scalar)
- Normal (Texture)
- AO (Texture)

### Notas
- Usa instancias para cada material.

## 2) Instancias de Material
- `MI_Dirt`
- `MI_Sand`
- `MI_Stone`
- `MI_Coal`
- `MI_Wood`

## 3) Aplicación rápida
- Asignar cada MI a los meshes placeholder de voxel o cubos.
