# Prop Modeling for Games

Create optimized 3D prop assets from concept to engine-ready state.

---

## Pipeline Overview

```
Concept → Blockout → High-Poly → Retopology → UV → Bake → Texture → Engine
```

### Step 1: Blockout
- Match silhouette and proportions to concept
- Use simple shapes at correct scale
- Get approval before detailing

### Step 2: High-Poly
- Add all surface detail (bolts, seams, bevels)
- No polygon budget — quality normals are the goal
- All edges beveled for realistic light catching

### Step 3: Retopology

| Asset Type | Triangle Budget | Method |
|-----------|----------------|--------|
| Hero prop (held) | 5K-15K | Manual retopo |
| Background prop | 500-3K | Auto-retopo |
| Weapon | 8K-20K | Manual (precise for animation) |
| Vehicle | 20K-80K | Manual body, auto internals |

### Step 4: UV Unwrapping
- Maximize UV space usage (>85%)
- Minimize stretching (checker test)
- Place seams on hidden edges
- Consistent texel density

---

## Baking

### Maps to Bake

| Map | Source | Use |
|-----|--------|-----|
| Normal | High to low | Surface detail |
| AO | High-poly | Contact shadows |
| Curvature | From normals | Edge wear masks |
| Position | World/object space | Gradient effects |
| Thickness | Raycast | Translucency |

### Baking Settings
- Resolution: 2048 for hero, 1024 for background
- Cage distance: Just enough to cover high-poly
- Samples: 4-8 for clean results
- Software: Marmoset Toolbag (best), Substance Painter

### Common Problems

| Problem | Cause | Fix |
|---------|-------|-----|
| Seam artifacts | UV seam in bake | Add 16-32px padding |
| Ray misses | Cage too tight | Increase cage distance |
| Waviness | Low too different from high | Better retopology |
| Projection errors | Misaligned meshes | Check alignment |

---

## LOD Creation

| LOD | % of LOD0 | Method |
|-----|----------|--------|
| LOD0 | 100% | Hand-crafted |
| LOD1 | 50% | Simplygon or manual |
| LOD2 | 25% | Auto-reduce |
| LOD3 | 10% | Aggressive auto |

- Maintain silhouette at all levels
- Same UV layout for all LODs
- Test at intended viewing distances
