# Memory Optimization for Rendering

Manage GPU and system memory efficiently for real-time rendering applications.

---

## Memory Budget Planning

### Platform Memory Budgets

| Platform | Total GPU VRAM | Rendering Budget | Texture Budget | Buffer Budget |
|----------|---------------|-----------------|----------------|---------------|
| Mobile (low) | 1-2 GB shared | 200-400 MB | 150-300 MB | 50-100 MB |
| Mobile (high) | 4-6 GB shared | 500-800 MB | 400-600 MB | 100-200 MB |
| Desktop (mid) | 6-8 GB | 2-3 GB | 1.5-2 GB | 500 MB |
| Desktop (high) | 12-24 GB | 4-8 GB | 3-6 GB | 1-2 GB |
| Console | 8-16 GB shared | 3-6 GB | 2-4 GB | 500 MB-1 GB |

---

## Texture Memory Management

### Texture Compression

| Format | Ratio | Quality | Platform |
|--------|-------|---------|----------|
| BC1/DXT1 | 6:1 | Low (no alpha) | Desktop, console |
| BC3/DXT5 | 4:1 | Good (with alpha) | Desktop, console |
| BC7 | 3:1 | Excellent | Desktop, modern console |
| ASTC 4x4 | 4:1 | Excellent | Mobile, console |
| ASTC 8x8 | 16:1 | Good | Mobile (aggressive) |
| ETC2 | 4:1 | Good | Android, WebGL |

### Texture Streaming

Load textures at appropriate resolution based on distance and visibility:

**Streaming Pipeline:**
1. Determine required mip level based on screen coverage
2. If required mip not in memory, request load
3. Load from disk/network asynchronously
4. Upload to GPU when ready
5. Track usage, evict unused textures

**Priority System:**

| Priority | Description | Example |
|----------|-------------|---------|
| Critical | Currently visible, close | Player character textures |
| High | Visible, medium distance | Nearby environment |
| Medium | Visible, far | Distant terrain |
| Low | Not visible but nearby | Objects behind camera |
| Evict | Not used recently | Far-away, off-screen |

### Mipmap Strategies
- Always generate mipmaps for 3D scene textures
- Skip mipmaps for UI textures, sprites at fixed size
- Use mip bias to intentionally use lower detail
- Consider mip streaming: load only needed mip levels

---

## Mesh and Buffer Memory

### Vertex Buffer Optimization

| Technique | Memory Savings | Quality Impact |
|-----------|---------------|----------------|
| Index buffers (16-bit) | 30-50% | None |
| Compressed vertex formats | 20-40% | Minimal |
| Shared vertex buffers | Reduces fragmentation | None |
| LOD systems | 50-90% for distant objects | Controlled |
| Mesh quantization | 30-50% | Slight precision loss |

### Vertex Format Compression

| Attribute | Full Format | Compressed | Savings |
|-----------|------------|------------|---------|
| Position | float3 (12B) | half3 (6B) or snorm16 | 50% |
| Normal | float3 (12B) | snorm8x4 (4B) octahedral | 67% |
| Tangent | float4 (16B) | snorm8x4 (4B) | 75% |
| UV | float2 (8B) | half2 (4B) or unorm16x2 | 50% |
| Color | float4 (16B) | unorm8x4 (4B) | 75% |

---

## Memory Pooling

### Pool Strategies

| Pool Type | Description | Use Case |
|-----------|-------------|----------|
| Ring buffer | Circular allocation, auto-free | Per-frame uniform data |
| Free list | Track free blocks, reuse | Dynamic mesh data |
| Buddy allocator | Power-of-2 blocks | GPU buffers |
| Stack allocator | LIFO allocation/free | Temporary render targets |

### Render Target Management
- Reuse render targets between passes (aliasing)
- Use transient render targets when possible
- Match render target resolution to output need
- Consider half-resolution for effects (SSAO, bloom)

---

## Memory Profiling

### Tools

| Tool | Platform | Features |
|------|----------|----------|
| RenderDoc | Cross-platform | Texture/buffer inspection |
| NSight | NVIDIA | Detailed VRAM tracking |
| Xcode Memory Graph | Apple | Metal resource tracking |
| PIX | Windows | DirectX resource analysis |
| GPU-Z | Desktop | Real-time VRAM monitoring |

### Key Metrics to Monitor

| Metric | Warning | Critical |
|--------|---------|----------|
| VRAM usage | > 70% budget | > 90% budget |
| Texture memory | > 60% of VRAM | > 80% of VRAM |
| Allocation rate | > 100 allocs/frame | > 500 allocs/frame |
| Fragmentation | > 20% | > 40% |
| Streaming latency | > 100ms | > 500ms |
