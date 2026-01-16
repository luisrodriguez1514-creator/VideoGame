# Diseño inicial: Mundo abierto procedural (Unreal Engine 5)

## Objetivo
Construir un prototipo base estilo “Minecraft realista” en UE5 con:
- Mundo procedural por semillas.
- Recolección de recursos básicos (tierra, arena, piedra, carbón, madera).
- Árboles con rebrote.
- Mesa de crafteo.
- Personaje por defecto con animaciones y herramientas.

---

## 1) Generación de mundo procedural por semillas
**Meta:** El mundo se genera a partir de una semilla. Si el jugador no ingresa una, el juego genera una aleatoria y la muestra en pantalla/menú para compartirla.

**Propuesta técnica (UE5):**
- **Sistema de semillas**
  - Si el jugador no ingresa una semilla, se genera con `FMath::Rand()` o `FMath::RandRange()` y se guarda.
  - Se muestra la semilla usada en UI (pantalla de creación o HUD).
- **Ruido para el terreno**
  - Usar Perlin/Simplex (FastNoise, ProceduralMesh, o plugin de ruido).
  - Parametrizar: altura base, frecuencia, amplitud, rugosidad.
- **Biomas básicos iniciales**
  - Llanura y dunas (arena).
  - Separación por altura y/o temperatura (más adelante).

**Resultado esperado:** Un mapa consistente que se repite siempre con la misma semilla.

---

## 2) Materiales básicos y excavación
**Materiales iniciales:**
- Tierra
- Arena
- Piedra
- Carbón
- Madera

**Reglas de recolección:**
- Al excavar/bloquear, dar el item correspondiente:
  - Tierra → “Bolsa de tierra”
  - Arena → “Arena”
  - Piedra → “Piedra”
  - Carbón → “Carbón”
- Profundidad:
  - Superficie: tierra/arena.
  - Debajo: piedra.
  - Carbón en vetas raras dentro de piedra.

---

## 3) Árboles
**Árbol único inicial** (1 tipo):
- Al talar:
  - Entrega X madera.
  - Deja un rebrote (sapling) para replantar.

---

## 4) Mesa de crafteo y recetas iniciales
**Mesa de crafteo:**
- Requiere madera (2) y piedra (2).

**Herramientas iniciales:**
| Herramienta | Materiales propuestos | Daño base | Uso |
|-----------|-----------------------|----------|-----|
| Hacha     | 2 madera + 5 piedra   | 10       | Talado rápido |
| Pico      | 2 madera + 6 piedra   | 12       | Minería rápida |
| Pala      | 2 madera + 4 piedra   | 6        | Excavación rápida |
| Espada    | 2 madera + 8 piedra   | 15       | Combate |

**Nota:** Estos valores son ajustables según feedback.

---

## 5) Personaje por defecto y animaciones
**Personaje base:**
- Usar el Mannequin de UE5.

**Animaciones mínimas:**
- Caminar
- Correr
- Saltar
- Agacharse
- Golpear
- Usar herramientas (hacha, pico, pala)
- Usar espada

---

## 6) Roadmap propuesto (primeras iteraciones)
1. **Mundo procedural** con semillas + UI de seed.
2. **Sistema de bloques** (tierra/arena/piedra/carbón) y recolección.
3. **Árboles** con loot y rebrote.
4. **Mesa de crafteo** + recetas iniciales.
5. **Personaje y animaciones** con herramientas básicas.

---

## 7) Próximos pasos
Si este plan te gusta, el siguiente paso sería elegir:
- Si el terreno será **voxel** (tipo Minecraft) o **mesh procedural**.
- Qué plugin o sistema de ruido usar.
- Definir tamaños de chunk y optimización.

Con esto arrancamos una base sólida para extender biomeas, animales, estructuras y más.
