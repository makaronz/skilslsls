# Environment Asset Creation

Build modular environment pieces for game level design.

---

## Modular Design

### Grid System
- Base grid: 1m, 2m, or 4m
- All pieces snap to grid perfectly
- Consistent pivot points (bottom-center)

### Kit Components

| Category | Pieces | Alignment |
|----------|--------|-----------|
| Walls | Straight, corner, T-junction, end cap | 1-4m lengths |
| Floors | Flat, stairs, ramp, platform | Grid-aligned |
| Pillars | Structural, decorative | Corner placement |
| Trim | Baseboards, crown molding | Edge-aligned |
| Doors/Windows | Standard openings | Wall-integrated |
| Props | Furniture, debris | Free placement |

### Connection Standards
- Vertices align exactly at boundaries
- Matching normals at connections
- UV seams at module boundaries
- Consistent texture scale

---

## Trim Sheet Workflow

1. Identify repeating details (molding, panels, edges)
2. Model each as a horizontal strip
3. Arrange on single texture
4. Bake normals and PBR textures
5. UV map modules to sample from trim sheet

---

## Vegetation

### Tree Creation Methods
| Method | Quality | Performance |
|--------|---------|------------|
| Hand-modeled | Best | Varies |
| SpeedTree | Very good | Optimized |
| Billboard cross | Low | Very fast |
| Impostor | Good at distance | Very fast |

### Foliage Optimization
- Alpha-tested cutout for leaves
- Reduce count at distance (LOD)
- Bake leaf clusters for LOD1+
- Wind via vertex color + shader
- Atlas all textures on single sheet

---

## Optimization Checklist

- [ ] Modules snap to grid cleanly
- [ ] No Z-fighting at connections
- [ ] Consistent texel density
- [ ] LODs for significant poly count pieces
- [ ] Lightmap UVs non-overlapping
- [ ] Collision meshes simplified
- [ ] Materials batched where possible
- [ ] Tested at target frame rate
