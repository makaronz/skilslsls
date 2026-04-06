# Culling Techniques

Remove invisible geometry before rendering to maximize GPU efficiency.

---

## Culling Pipeline

```
All Objects → Frustum Culling → Occlusion Culling → LOD Selection
  → Distance Culling → Contribution Culling → Final Render List
```

---

## Frustum Culling

Reject objects outside the camera's view frustum (6 planes: near, far, left, right, top, bottom).

### Implementation

**Bounding Volume Tests:**

| Volume | Test Cost | Tightness | Best For |
|--------|----------|-----------|----------|
| Sphere | Very fast (1 dot product/plane) | Loose | First pass, round objects |
| AABB | Fast (3 axis tests) | Medium | Axis-aligned objects |
| OBB | Moderate | Tight | Rotated objects |
| Convex hull | Slow | Very tight | Complex, important objects |

**Hierarchical Frustum Culling:**
1. Test scene bounding volume
2. Traverse spatial hierarchy (BVH, octree, quadtree)
3. If parent node is outside frustum, skip all children
4. If parent is inside, all children are inside (skip per-child test)
5. If parent intersects, test children individually

### Spatial Data Structures

| Structure | Best For | Insert/Remove | Query |
|-----------|---------|---------------|-------|
| Octree | Static 3D scenes | O(log n) | O(log n) |
| BVH (Bounding Volume Hierarchy) | Dynamic scenes | Refit: O(n) | O(log n) |
| Quadtree | Terrain, 2D layouts | O(log n) | O(log n) |
| Grid | Uniform density | O(1) | O(1) per cell |
| k-d Tree | Point clouds | O(n log n) build | O(log n) |

---

## Occlusion Culling

Reject objects hidden behind other objects.

### Software Occlusion Culling
1. Render simplified occluder meshes to CPU depth buffer
2. Test occludee bounding boxes against depth buffer
3. If fully occluded, skip rendering

**Occluder Selection:**
- Large, solid objects (walls, floors, buildings)
- Low-poly simplified versions for CPU testing
- Pre-tag in editor or auto-detect based on surface area

### Hardware Occlusion Queries
1. Render bounding box with color/depth writes disabled
2. GPU returns pixel count that passed depth test
3. If zero pixels visible, skip full render next frame

**Drawback:** 1-frame latency (query returns next frame)
**Mitigation:** Use previous frame's results + conservative bounds

### Hierarchical Z-Buffer (Hi-Z)
- Mipmap chain of depth buffer
- Test bounding box against appropriate mip level
- Very fast rejection of large occluded areas
- GPU-accelerated in modern engines

---

## Level of Detail (LOD)

Reduce geometric complexity based on distance or screen coverage.

### LOD Strategy

| LOD Level | Distance | Triangle % | Visual Quality |
|-----------|----------|-----------|---------------|
| LOD0 | Near (< 10m) | 100% | Full detail |
| LOD1 | Medium (10-30m) | 50% | Slight simplification |
| LOD2 | Far (30-80m) | 25% | Noticeable but acceptable |
| LOD3 | Very far (80m+) | 10% | Silhouette only |
| Billboard | Extreme | 2 triangles | Imposter image |

### LOD Transition Methods

| Method | Visual Quality | Performance | Complexity |
|--------|---------------|-------------|-----------|
| Discrete (pop) | Visible pop | Fast switch | Simple |
| Cross-fade (dithered) | Smooth | Double render briefly | Medium |
| Morph targets | Smooth | GPU interpolation | Complex |
| Screen-size based | Adaptive | Resolution-aware | Medium |

### Automatic LOD Generation
- **Mesh simplification**: Reduce triangles while preserving shape
- **Algorithms**: Quadric error metrics, edge collapse
- **Tools**: Simplygon, InstaLOD, open-source MeshLab
- **Targets**: 50% reduction per LOD level

---

## Distance and Contribution Culling

### Distance Culling
- Set maximum render distance per object type
- Small objects: cull at shorter distances
- Important objects (characters, objectives): longer distances
- Fade out before culling to avoid popping

### Contribution Culling
- Calculate object's screen-space size (pixels)
- If below threshold (e.g., < 2 pixels), don't render
- More accurate than pure distance (accounts for camera FOV)

```
screen_size = (object_radius / distance_to_camera) * screen_height / (2 * tan(fov/2))
if screen_size < min_pixel_threshold:
    skip rendering
```
