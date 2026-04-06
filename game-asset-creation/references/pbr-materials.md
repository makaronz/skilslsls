# PBR Materials for Game Assets

Create physically-based rendering materials using metallic-roughness workflow.

---

## PBR Maps

| Map | Description | Value Range |
|-----|-------------|-------------|
| Base Color | Surface color without lighting | sRGB, 30-240 |
| Metallic | Metal vs non-metal | 0.0 or 1.0 (binary) |
| Roughness | Surface smoothness | 0.0 (mirror) to 1.0 (rough) |
| Normal | Surface detail bumps | Tangent space |
| AO | Contact shadows | 0.0-1.0 |
| Emissive | Self-illumination | Any brightness |

### Material Reference Values

| Material | Base Color | Metallic | Roughness |
|----------|-----------|----------|-----------|
| Dark soil | 30-50 sRGB | 0.0 | 0.8-1.0 |
| Plastic | 50-200 sRGB | 0.0 | 0.3-0.6 |
| Gold | 255,200,50 | 1.0 | 0.2-0.4 |
| Iron | 186,186,186 | 1.0 | 0.4-0.7 |
| Chrome | 230,230,230 | 1.0 | 0.0-0.1 |

---

## Substance Painter Workflow

### Layer Organization
```
Final Adjustments (levels, color balance)
├── Dust/Dirt (generator-based)
├── Scratches/Wear (curvature + paint)
├── Decals/Labels (stencils)
├── Material: Metal (fill + smart mask)
├── Material: Paint (fill + smart mask)
└── Base Color (overall flat)
```

### Smart Mask Generators
| Generator | Input | Use |
|-----------|-------|-----|
| Metal Edge Wear | Curvature | Exposed metal under paint |
| Dirt | AO + Position | Grime in crevices |
| Light | Position | Top-down weathering |
| Moisture | AO + curvature | Wet areas |

---

## Texture Resolution

| Asset Type | Resolution |
|-----------|-----------|
| Hero prop | 2048x2048 |
| Standard prop | 1024x1024 |
| Background prop | 512x512 |
| Character | 2048 per region |

---

## Engine Export

### Unreal Engine
| Map | sRGB |
|-----|------|
| Base Color | Yes |
| Normal (DirectX) | No |
| ORM packed | No |

### Unity
| Map | Notes |
|-----|-------|
| Base Map | sRGB |
| Normal (OpenGL) | Linear |
| Metallic + Smoothness(A) | Linear, invert roughness |
