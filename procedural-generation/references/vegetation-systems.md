# Vegetation Systems

Procedurally generate and place realistic vegetation for games and simulations.

---

## L-Systems (Lindenmayer Systems)

### Fundamentals

L-systems use string rewriting rules to generate branching structures:

**Components:**
| Symbol | Meaning |
|--------|---------|
| F | Draw forward |
| + | Turn right |
| - | Turn left |
| [ | Save state (push) |
| ] | Restore state (pop) |
| & | Pitch down |
| ^ | Pitch up |
| \\ | Roll left |
| / | Roll right |

### Example: Simple Tree

```
Axiom: F
Rule: F → F[+F]F[-F][F]
Iterations: 4
Angle: 25°
```

### Stochastic L-Systems

Add randomness for natural variation:
- Randomize branch angles (±5-15°)
- Randomize segment lengths (±10-20%)
- Multiple rules with probability weights
- Random pruning (skip branches with probability)

---

## Tree Generation

### Space Colonization Algorithm

More realistic than L-systems for mature trees:

1. Place attraction points in desired crown shape (sphere, cone, custom)
2. Find nearest branch node for each attraction point
3. Grow branch toward nearby attraction points
4. Remove attraction points reached by branches
5. Repeat until all points consumed or max iterations

**Parameters:**
| Parameter | Effect | Typical Value |
|-----------|--------|--------------|
| Kill distance | When to remove attraction points | 1-5 units |
| Influence distance | Max distance points affect growth | 10-50 units |
| Growth step | Branch segment length | 0.5-2 units |
| Crown shape | Overall tree silhouette | Sphere, cone, hemisphere |
| Point density | Branch density/detail | 500-5000 points |

### Tree Species Variation

| Species Style | Crown Shape | Branch Angle | Trunk Character |
|--------------|-------------|-------------|----------------|
| Oak | Wide sphere | 30-60° | Thick, gnarled |
| Pine | Tall cone | 60-80° | Straight, minimal |
| Willow | Drooping hemisphere | 20-40° + gravity | Moderate |
| Palm | Radial fan at top | N/A (fronds) | Tall, curved |
| Birch | Narrow ellipse | 30-50° | Thin, white bark |

---

## Vegetation Placement

### Distribution Algorithms

| Algorithm | Pattern | Control | Performance |
|-----------|---------|---------|-------------|
| Poisson Disk | Uniform spacing, natural | Minimum distance | Fast (Bridson's) |
| Blue noise | Uniform, no clustering | Frequency control | Fast |
| Scatter + rules | Rule-based placement | High (slope, height, biome) | Medium |
| Ecosystem simulation | Competitive growth | Very realistic | Slow (precompute) |
| Hand-painted + procedural | Artist-guided | Maximum | Fast runtime |

### Poisson Disk Sampling (Bridson's Algorithm)

Fast O(n) algorithm for natural-looking placement:

1. Choose initial sample point
2. For each active sample, generate k candidates at distance [r, 2r]
3. Keep candidates that are >r from all existing samples
4. If no valid candidate after k tries, deactivate sample
5. Repeat until no active samples remain

### Biome-Based Rules

| Rule | Example |
|------|---------|
| Height | Trees below tree line, grass above |
| Slope | No trees on steep slopes (>35°) |
| Moisture | Dense vegetation near water |
| Sunlight | Shade-tolerant species under canopy |
| Soil type | Different species for different terrain |
| Proximity | Minimum spacing between trees |
| Density | Gradual transition between biomes |

---

## LOD for Vegetation

| LOD Level | Technique | Distance | Memory |
|-----------|-----------|----------|--------|
| LOD0 | Full 3D mesh | < 20m | High |
| LOD1 | Simplified mesh | 20-50m | Medium |
| LOD2 | Billboard cross (2-3 planes) | 50-150m | Low |
| LOD3 | Single billboard | 150-500m | Very low |
| LOD4 | Point/removed | > 500m | None |

### Billboard Techniques
- **Cross billboard**: 2-3 intersecting planes with alpha texture
- **Axial billboard**: Rotates on Y-axis to face camera
- **Impostor**: Pre-rendered from multiple angles, select nearest
- **Octahedral impostor**: 8+ views mapped to hemisphere

---

## Optimization

### GPU Instancing for Vegetation
- Group same species/LOD into instance buffers
- Per-instance data: position, rotation, scale, color variation
- Wind animation: Vertex displacement in shader using world position + time
- Typical scenes: 10K-100K instances, 10-50 draw calls

### Wind Animation
```hlsl
// Simple wind vertex displacement
float wind = sin(time * windSpeed + worldPos.x * 0.1 + worldPos.z * 0.1);
float windStrength = vertexHeight * windBendAmount;
worldPos.x += wind * windStrength;
```
