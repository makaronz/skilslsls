# Draw Call Optimization

Reduce CPU overhead from draw calls to maximize rendering throughput.

---

## Understanding Draw Calls

A draw call is a CPU command telling the GPU to render geometry. Each draw call has overhead:

| Component | CPU Cost | Optimization |
|-----------|----------|-------------|
| State changes | High | Sort by state, minimize switches |
| Buffer binds | Medium | Use shared buffers, instancing |
| Shader switches | High | Sort by shader |
| Texture binds | Medium | Atlasing, texture arrays |
| Uniform updates | Low-Medium | Uniform buffer objects |
| The draw call itself | Low | Batch, instance, indirect |

### Draw Call Budgets

| Platform | Target Draw Calls/Frame | Notes |
|----------|------------------------|-------|
| Mobile | 100-300 | CPU-limited, minimize at all costs |
| Desktop | 2,000-5,000 | Modern APIs handle more |
| Console | 3,000-10,000 | Efficient command buffers |
| VR (per eye) | 500-1,500 | Must render twice |

---

## Batching Techniques

### Static Batching
Combine meshes that never move into single buffers at build time.

**When to Use:** Static environment props, terrain decorations, buildings

**Implementation:**
1. Identify objects sharing the same material
2. Merge vertex/index buffers at build time
3. Store combined mesh as single drawable
4. Trade memory for fewer draw calls

### Dynamic Batching
Combine small, moving meshes at runtime.

**Rules:**
- Objects must share same material/shader
- Typically limited to <300 vertices per mesh
- CPU cost of merging must be less than draw call savings
- Most effective for particles, UI elements, small props

### GPU Instancing

Render many copies of the same mesh with per-instance data:

```hlsl
// Instance data buffer
struct InstanceData {
    float4x4 transform;
    float4 color;
    float2 uvOffset;
};

// Vertex shader reads per-instance data
float4x4 worldMatrix = instanceBuffer[instanceID].transform;
```

**Best For:** Trees, grass, rocks, crowds, bullets — any repeated geometry

| Count | Without Instancing | With Instancing |
|-------|-------------------|----------------|
| 1,000 trees | 1,000 draw calls | 1 draw call |
| 10,000 grass | 10,000 draw calls | 1-10 draw calls |

### Indirect Rendering (GPU-Driven)

GPU determines what and how much to draw:

```
// CPU: Submit single indirect draw
// GPU: Fills argument buffer with instance counts
// GPU: Executes draws based on visibility results
```

**Benefits:**
- GPU-based culling reduces CPU involvement
- Zero CPU overhead for per-object visibility
- Scales to millions of objects

---

## State Change Reduction

### Sort Order Priority

Sort draw calls to minimize state changes:

```
1. Render target / framebuffer
2. Shader / pipeline state
3. Material / texture set
4. Geometry buffer
5. Per-object uniforms
```

### Material Merging Strategies

| Strategy | Description | Complexity |
|----------|-------------|-----------|
| Texture atlas | Combine textures, adjust UVs | Low |
| Uber shader | Single shader with feature toggles | Medium |
| Material arrays | Array of parameters, index per instance | Medium |
| Bindless textures | GPU handles to all textures | High |

---

## Profiling Draw Call Performance

### What to Measure

| Metric | Tool | Target |
|--------|------|--------|
| Total draw calls | Frame debugger | Within budget |
| CPU time in rendering | CPU profiler | < 5ms |
| State change count | API tracer | Minimize |
| Overdraw percentage | Visualization mode | < 2x average |
| Triangle count | Stats overlay | Within budget |

### Optimization Workflow
1. Profile current frame → identify draw call count
2. Sort render list by shader → material → mesh
3. Enable static batching for immovable objects
4. Enable instancing for repeated objects
5. Implement LOD to reduce distant object complexity
6. Re-profile → verify improvement
