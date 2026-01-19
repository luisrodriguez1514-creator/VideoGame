# Diseño del proyecto: Mundo abierto procedural (Unreal Engine 5)

## Objetivo
Construir un prototipo base estilo “Minecraft realista” en UE5 con:
- Mundo procedural por semillas.
- Recolección de recursos básicos (tierra, arena, piedra, carbón, madera).
- Árboles con rebrote.
- Mesa de crafteo.
- Personaje por defecto con animaciones y herramientas.

---

## 1) Visión general del proyecto
**Nombre (provisional):** RealistaCraft

**Pilares del diseño:**
1. **Exploración procedural**: mundos reproducibles por semilla.
2. **Supervivencia ligera**: recolección, crafteo y herramientas básicas.
3. **Interacción del mundo**: excavar, talar, picar con feedback inmediato.
4. **Realismo visual moderado**: iluminación y materiales más realistas que Minecraft.

---

## 2) Alcance del MVP (primera versión jugable)
**Incluye:**
- Terreno procedural por semillas con 2 biomas iniciales (llanura/arena).
- Bloques base: tierra, arena, piedra, carbón.
- Árbol único con rebrote.
- Inventario simple (stacking básico).
- Mesa de crafteo con recetas iniciales.
- Herramientas: hacha, pico, pala, espada.
- Personaje por defecto con animaciones y uso de herramientas.
- Sistema de supervivencia desde el inicio: hambre, sed y vida por defecto.

**No incluye (por ahora):**
- Animales/NPCs.
- Construcción avanzada.

---

## 3) Arquitectura técnica propuesta (UE5)

### 3.1 Sistema de semillas
- Entrada de semilla en UI (pantalla inicial).
- Si no hay semilla, se genera con `FMath::Rand()` y se guarda.
- Se muestra la semilla usada en HUD.

### 3.2 Generación de mundo
**Opción definida:** Voxel basado en chunks.
- **Chunk**: 32x32x128 (seleccionado para equilibrar detalle y costo de generación; validaremos rendimiento).
- **Ruido**: Perlin/Simplex con **FastNoise2** (plugin obligatorio).
- **Datos**: mapa de altura + capas por tipo de bloque.
- **LOD/optimización**: generación por distancia al jugador.

### 3.3 Sistema de bloques
- Cada bloque tiene:
  - Tipo (tierra/arena/piedra/carbón)
  - Resistencia
  - Loot asociado
- Al romper un bloque, se genera el item correspondiente.

### 3.4 Inventario y loot
- Inventario en UI con stacks por item.
- Loot directo a inventario si hay espacio.
- Items base: tierra, arena, piedra, carbón, madera, rebrote.

### 3.5 Árboles y rebrote
- Árbol único con reglas simples:
  - Talado da madera.
  - Cae un rebrote para replantar.
- Replantación en tierra válida.

### 3.6 Crafteo
- Mesa de crafteo como actor interactivo.
- Recetas en `DataTable` o `PrimaryDataAsset`.
- UI de crafteo simple con slots.

### 3.7 Combate, herramientas y supervivencia
- Herramientas con daño y eficiencia.
- Sistema de golpes con trazas (line trace / sphere trace).
- Durabilidad simple (opcional para MVP).
- Sistema de supervivencia inicial:
  - Hambre y sed con decremento por tiempo/acciones.
  - Vida base (HP) con regeneración limitada.

---

## 4) Diseño de contenido inicial

### 4.1 Materiales básicos
- Tierra → “Bolsa de tierra”
- Arena → “Arena”
- Piedra → “Piedra”
- Carbón → “Carbón”
- Madera → “Madera”
- Rebrote → “Semilla de árbol”

### 4.2 Recetas iniciales
| Item | Materiales | Resultado |
|------|------------|-----------|
| Mesa de crafteo | 2 madera + 2 piedra | 1 mesa |
| Hacha | 2 madera + 5 piedra | 1 hacha |
| Pico | 2 madera + 6 piedra | 1 pico |
| Pala | 2 madera + 4 piedra | 1 pala |
| Espada | 2 madera + 8 piedra | 1 espada |

### 4.3 Daño base y eficiencia
- Hacha: daño 10, +50% eficiencia al talar árboles.
- Pico: daño 12, +50% eficiencia al minar piedra/carbón.
- Pala: daño 6, +50% eficiencia al excavar tierra/arena.
- Espada: daño 15 (combate).

---

## 5) Personaje y animaciones
- Usar el **Mannequin de UE5**.
- Animaciones mínimas:
  - Caminar, correr, saltar, agacharse.
  - Golpear.
  - Usar herramientas (hacha, pico, pala, espada).

---

## 6) Estructura de carpetas recomendada
```
Content/
  Blueprints/
    Player/
    World/
    Items/
    UI/
  Data/
    Items/
    Recipes/
  Materials/
  Meshes/
  Animations/
```

---

## 7) Roadmap propuesto
1. **Semana 1-2**: Sistema de semillas + terreno procedural básico.
2. **Semana 3**: Bloques base y recolección.
3. **Semana 4**: Árboles, loot y rebrote.
4. **Semana 5**: Inventario simple y crafteo.
5. **Semana 6**: Herramientas, animaciones y combate básico.

---

## 8) Próximos pasos
- Validar tamaño de chunk con pruebas de rendimiento.
- Definir estilo visual de **voxel realista** (materiales PBR, iluminación).
- Planear arquitectura para **multijugador futuro** (replicación y determinismo).

---

## 9) Preguntas abiertas
- Penalizaciones por hambre y sed:
  - **Hambre**: efecto negativo de hambre → mareo y fatiga → pérdida gradual de vida hasta morir.
  - **Sed**: efecto de insolación → pérdida gradual de vida hasta morir.
- Escala inicial del mundo: **5,000 x 5,000 metros** antes de requerir streaming avanzado.

Con este diseño, podemos iniciar implementación de los sistemas base y ajustar sobre la marcha.
