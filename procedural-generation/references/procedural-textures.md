# Procedural Textures

Generate textures algorithmically for infinite variety and resolution independence.

---

## Core Patterns

### Noise-Based Textures

| Texture | Noise Type | Parameters | Use Case |
|---------|-----------|-----------|----------|
| Marble | Perlin + sin wave | Turbulence, color mapping | Stone, marble surfaces |
| Wood grain | Cylindrical noise | Ring frequency, distortion | Wooden objects |
| Cloud/smoke | fBm | Octaves, gain, threshold | Sky, fog, smoke |
| Terrain color | fBm + biome map | Height, moisture | Ground textures |
| Water caustics | Voronoi + animation | Cell density, time | Water surfaces |

### Mathematical Patterns

| Pattern | Algorithm | Control Parameters |
|---------|-----------|-------------------|
| Voronoi cells | Nearest seed point distance | Cell density, distance metric |
| Worley noise | Nth-nearest point distance | F1, F2 distances, combination |
| Checkerboard | `floor(x) + floor(y) % 2` | Scale, colors |
| Brick | Offset rows + mortar | Brick size, mortar width, offset |
| Hexagonal grid | Axial coordinates | Cell size, border width |
| Dots/halftone | Distance from grid centers | Dot radius, grid spacing |

---

## Substance-Style Node Graphs

### Common Node Types

| Category | Nodes | Purpose |
|----------|-------|---------|
| Generators | Noise, gradient, shape | Base patterns |
| Filters | Blur, sharpen, warp, levels | Modify patterns |
| Blend | Add, multiply, overlay, max | Combine patterns |
| Transform | Scale, rotate, tile | Spatial manipulation |
| Color | HSL adjust, gradient map | Color mapping |
| Normal | Normal from height, combine | Normal map generation |

### Workflow: Creating a Brick Wall Texture

1. **Base shape**: Rectangular tile generator with offset rows
2. **Height variation**: Add noise to brick surfaces
3. **Mortar**: Invert and expand gaps between bricks
4. **Weathering**: Blend edge damage using curvature + noise mask
5. **Color**: Gradient map with brick color variations
6. **Normal map**: Convert height to normal map
7. **Roughness**: Derive from mortar vs brick surfaces

---

## PBR Texture Generation

### Channel Generation

| PBR Channel | Generation Method | Value Range |
|-------------|------------------|-------------|
| Base Color (Albedo) | Color mapping of patterns | sRGB, 0-1 |
| Normal Map | Height → normal conversion | Tangent space, -1 to 1 |
| Roughness | Pattern-based (rough/smooth areas) | Linear, 0-1 |
| Metallic | Binary mask (metal vs non-metal) | 0.0 or 1.0 (usually) |
| Height/Displacement | Raw height pattern | Linear, 0-1 |
| Ambient Occlusion | Cavity detection from height | Linear, 0-1 |

### Material Blending

Blend multiple material layers using height-based masking:
```
blend_factor = smoothstep(threshold - blend, threshold + blend, height_mask + noise)
final_color = mix(material_A, material_B, blend_factor)
```

---

## Optimization

### Tiling and Seams
- Use tileable noise (wrap coordinates in noise space)
- Histogram-preserving blending for non-repeating tiling
- Wang tiles for varied tiling without obvious repeats

### Runtime Generation
- Generate on GPU using compute shaders
- Cache generated textures to disk/memory
- Use texture arrays for procedural material variants
- Virtual texturing for on-demand generation at needed resolution

### Quality Tips
- Add micro-detail noise to prevent plastic look
- Vary hue slightly across surface for natural appearance
- Use reference photos to calibrate noise parameters
- Test at multiple viewing distances and lighting conditions
