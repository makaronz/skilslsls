# Shader Optimization

Optimize GPU shaders for real-time rendering performance across platforms.

---

## Shader Performance Fundamentals

### GPU Pipeline Stages

| Stage | Bottleneck Indicator | Optimization Focus |
|-------|---------------------|-------------------|
| Vertex Shader | High vertex count, complex transforms | Reduce vertex count, simplify math |
| Rasterizer | Many small triangles, high overdraw | LOD, culling, larger triangles |
| Fragment Shader | Complex pixel operations, many textures | Simplify math, reduce texture reads |
| Output Merger | High blend cost, many render targets | Reduce transparency, minimize MRTs |

### Profiling Tools

| Tool | Platform | Capabilities |
|------|----------|-------------|
| RenderDoc | Cross-platform | Frame capture, shader debugging |
| NSight Graphics | NVIDIA | Detailed GPU profiling |
| PIX | Windows/Xbox | DirectX profiling |
| Xcode GPU Profiler | Apple | Metal shader profiling |
| Mali Offline Compiler | ARM | Mobile GPU analysis |

---

## Optimization Techniques

### Math Optimizations

| Optimization | Before | After | Savings |
|-------------|--------|-------|---------|
| Normalize in vertex shader | Per-pixel normalize | Interpolate normalized vectors | 50%+ fragment ALU |
| Use half precision | `float` everywhere | `half` for color, UV | 2x throughput on mobile |
| Approximate functions | `pow(x, 5.0)` | `x * x * x * x * x` | 3-5 cycles |
| MAD operations | `a * b + c` (separate) | `mad(a, b, c)` | Hardware optimized |
| Avoid branches | `if (x > 0)` | `step(0, x) * value` | Eliminates divergence |
| Pack data | 4 separate floats | float4 vector | Single register |

### Texture Optimization

| Technique | Description | Impact |
|-----------|-------------|--------|
| Mipmapping | Pre-computed lower resolutions | Reduces bandwidth, removes aliasing |
| Texture atlasing | Combine textures into one | Fewer state changes |
| Compressed formats | BC7, ASTC, ETC2 | 4-8x memory reduction |
| Channel packing | Pack data into RGBA channels | Fewer texture reads |
| Texture arrays | Same-size textures in array | Single bind call |

### Overdraw Reduction

Overdraw occurs when pixels are shaded multiple times:

1. **Front-to-back rendering**: Sort opaque objects by distance
2. **Early-Z rejection**: Depth test before fragment shader
3. **Z-prepass**: Render depth first, then full shading
4. **Occlusion culling**: Skip objects behind others
5. **Stencil masking**: Limit shading to specific regions

---

## Platform-Specific Guidelines

### Mobile GPU Optimization (Tile-Based Rendering)

| Practice | Reason |
|----------|--------|
| Minimize render target switches | Each switch flushes tile memory |
| Use `half` precision liberally | Mobile ALUs are half-precision native |
| Avoid dependent texture reads | Extra latency on tile GPUs |
| Keep fragment shaders simple | Fill rate is the main bottleneck |
| Use ASTC compression | Best quality-per-bit on mobile |
| Limit alpha blending | Forces tile writeback and re-read |

### Desktop GPU Optimization

| Practice | Reason |
|----------|--------|
| Maximize GPU occupancy | Hide latency with parallel warps |
| Use compute shaders | More flexible than fixed pipeline |
| Minimize state changes | Group by shader, then material, then texture |
| Use indirect rendering | GPU-driven draw calls |
| Leverage async compute | Overlap compute and graphics work |

---

## Common Shader Patterns

### PBR Performance Tiers

| Tier | Features | Cost | Platform |
|------|----------|------|----------|
| Low | Lambert diffuse, no specular | Very low | Low-end mobile |
| Medium | Blinn-Phong, single light | Low | Mobile, web |
| High | Cook-Torrance BRDF, IBL | Medium | Desktop, console |
| Ultra | Subsurface, anisotropic, clearcoat | High | High-end desktop |

---

## Measurement and Targets

| Platform | Target FPS | Frame Budget | Fragment Budget |
|----------|-----------|-------------|----------------|
| Mobile | 30-60 | 16.6-33.3ms | 5-10ms |
| Desktop | 60-144 | 6.9-16.6ms | 3-8ms |
| VR | 72-120 | 8.3-13.8ms | 4-6ms |
| Console | 30-60 | 16.6-33.3ms | 5-10ms |
