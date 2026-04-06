# Game Engine Integration

Import and configure 3D assets for Unity and Unreal Engine.

---

## Export Formats

| Format | Features | Unity | Unreal |
|--------|----------|-------|--------|
| FBX | Mesh, animation, materials | Excellent | Excellent |
| glTF/GLB | PBR materials, compact | Good | Good |
| OBJ | Mesh + UVs only | Basic | Basic |

### FBX Settings
- Scale: 1 unit = 1cm (Unreal) or 1m (Unity)
- Up axis: Y-up or Z-up (match DCC tool)
- Export normals (don't recompute)

---

## Unreal Engine

### Import Settings
| Setting | Recommendation |
|---------|---------------|
| Auto Generate Collision | Off (use custom) |
| Generate Lightmap UVs | On (static objects) |
| Normal Import | Import Normals |

### Material Setup
- Base Color to Base Color pin
- Normal (DirectX) to Normal pin
- ORM packed: R=AO, G=Roughness, B=Metallic
- Enable Nanite for high-poly meshes (UE5)

---

## Unity

### Import Settings
| Setting | Recommendation |
|---------|---------------|
| Scale Factor | 1 |
| Mesh Compression | Off for hero |
| Generate Colliders | Off (add manually) |

### Material Setup (URP/HDRP)
- Albedo texture as Base Map
- Normal map (set type to Normal Map)
- Invert roughness for Smoothness
- AO as Occlusion Map

---

## Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Wrong scale | cm vs m mismatch | Check export scale |
| Bad normals | Wrong tangent space | DirectX vs OpenGL |
| Washed textures | sRGB/Linear mismatch | Color=sRGB, data=Linear |
| Visible seams | UV seam + normal split | Increase texture padding |
| Shadow artifacts | Bad lightmap UVs | Generate UV2, increase resolution |
