# Terrain Generation

Generate realistic terrains using noise functions, erosion simulation, and heightmap techniques.

---

## Noise Functions

### Perlin Noise
- Gradient noise producing smooth, natural-looking patterns
- Values range -1 to 1 (typically normalized to 0-1 for heightmaps)
- Controllable frequency and amplitude
- Tileable variants available for seamless world wrapping

### Simplex Noise (Preferred)
- Less directional artifacts than Perlin
- Better performance in higher dimensions
- Gradient calculation uses simplex lattice instead of hypercube
- OpenSimplex2 is the patent-free variant

### Fractal Brownian Motion (fBm)

Layer multiple octaves of noise for natural detail:

```python
def fbm(x, y, octaves=6, lacunarity=2.0, gain=0.5):
    value = 0.0
    amplitude = 1.0
    frequency = 1.0
    for _ in range(octaves):
        value += amplitude * noise(x * frequency, y * frequency)
        amplitude *= gain       # Each octave is quieter
        frequency *= lacunarity  # Each octave is higher frequency
    return value
```

| Parameter | Effect | Typical Range |
|-----------|--------|--------------|
| Octaves | Detail levels | 4-8 |
| Lacunarity | Frequency multiplier | 1.5-2.5 |
| Gain (persistence) | Amplitude multiplier | 0.3-0.6 |
| Base frequency | Overall scale | 0.001-0.01 |

### Domain Warping

Distort noise input coordinates for more organic results:
```
warpedHeight = fbm(x + fbm(x, y), y + fbm(x+5.2, y+1.3))
```
Creates flowing, river-like patterns and natural-looking terrain features.

---

## Erosion Simulation

### Hydraulic Erosion

Simulate water flow to create realistic terrain features:

**Algorithm (Particle-Based):**
1. Drop water particle at random position
2. Compute terrain gradient at particle position
3. Move particle downhill along gradient
4. Particle picks up sediment (erosion) based on:
   - Carrying capacity (speed × water × slope)
   - Current sediment load vs capacity
5. Deposit sediment when capacity decreases
6. Evaporate water over time
7. Repeat for thousands of particles

**Parameters:**

| Parameter | Effect | Range |
|-----------|--------|-------|
| Erosion rate | Material removal speed | 0.01-0.1 |
| Deposition rate | Sediment settling speed | 0.01-0.1 |
| Evaporation | Water lifetime | 0.01-0.05 |
| Particle lifetime | Iteration count | 30-100 steps |
| Inertia | Path smoothness | 0.0-1.0 |

### Thermal Erosion
- Material slides downhill when slope exceeds talus angle
- Creates scree slopes and smooths sharp peaks
- Simpler than hydraulic, good for secondary pass
- Typical talus angle: 30-45 degrees

---

## Biome Assignment

### Height + Moisture Map

| Moisture → | Dry | Medium | Wet |
|------------|-----|--------|-----|
| **High elevation** | Rocky peaks | Alpine meadow | Snow/glacier |
| **Medium** | Savanna | Forest | Rainforest |
| **Low** | Desert | Grassland | Swamp |
| **Below sea level** | — | — | Ocean/lake |

### Implementation
1. Generate height map (noise + erosion)
2. Generate moisture map (separate noise, influenced by distance to water)
3. Assign biome per vertex/tile based on height + moisture
4. Blend textures at biome boundaries

---

## Optimization for Real-Time

### Chunked Terrain
- Divide world into fixed-size chunks (e.g., 256×256)
- Generate chunks on demand around player
- Use LOD per chunk based on distance
- Stream chunks from background thread

### GPU Terrain Generation
- Compute shaders for noise generation
- GPU-based erosion simulation
- Tessellation for adaptive detail
- Virtual texturing for terrain materials
