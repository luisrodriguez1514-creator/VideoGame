# Configurar BP_WorldManager (Blueprint de Mundo)

> Objetivo: dejar listo un Blueprint de mundo para iniciar el proyecto y poder ver un terreno generado desde el primer Play.

## 1) Crear el Blueprint
1. En el Content Browser, ve a `Content/Blueprints/World`.
2. Click derecho → **Blueprint Class**.
3. Selecciona **Actor**.
4. Nómbralo: **BP_WorldManager**.

## 2) Variables requeridas
En **BP_WorldManager**, agrega:

| Nombre | Tipo | Valor por defecto | Detalle |
|---|---|---|---|
| `Seed` | Integer | 0 | Si es 0, se genera aleatoria. |
| `ChunkSizeX` | Integer | 32 | Dimensión X del chunk. |
| `ChunkSizeY` | Integer | 32 | Dimensión Y del chunk. |
| `ChunkSizeZ` | Integer | 128 | Dimensión Z del chunk. |
| `BlockSize` | Float | 100.0 | Tamaño del voxel (cm). |
| `WorldSizeMeters` | Integer | 5000 | Escala del mundo. |
| `NoiseFrequency` | Float | 0.002 | Ajuste inicial de ruido. |
| `NoiseAmplitude` | Float | 2000.0 | Altura máxima. |

## 3) Lógica en BeginPlay
En el **Event Graph**:
1. `Event BeginPlay`
2. Si `Seed == 0` → `Set Seed` = `Random Integer in Range` (por ejemplo 1 a 999999).
3. Llama a un **Custom Event** llamado `GenerateInitialChunk`.

## 4) Generación mínima (placeholder visual)
Para validar rápido que todo funciona sin el sistema voxel completo:
1. En el `GenerateInitialChunk`, agrega un **Add Static Mesh Component**.
2. Usa el mesh `SM_Cube` (Engine/BasicShapes/Cube).
3. Escala el cubo a `BlockSize / 100.0` en XYZ.
4. Coloca el cubo en `(0,0,0)`.

> Esto solo sirve para verificar que el Actor funciona. Luego se reemplaza por chunks reales.

## 5) Colocar el Blueprint en el nivel
1. Abre el mapa principal (o crea uno nuevo).
2. Arrastra **BP_WorldManager** al mundo.
3. Presiona **Play** para validar que el cubo aparece en el origen.

## 6) Siguiente paso
Cuando confirmes que el mundo inicia bien, creamos:
- **BP_Chunk** con generación voxel.
- Integración con **FastNoise2**.
- Streaming por distancia.
