# Particle System Optimization

Maximize visual quality while maintaining frame rate budgets for particle effects.

---

## Performance Budget

### Per-Frame Budget Allocation

| Component | Mobile Budget | Desktop Budget | VR Budget |
|-----------|-------------|----------------|-----------|
| Total particles | 5,000-10,000 | 50,000-200,000 | 20,000-50,000 |
| Draw calls for particles | 10-30 | 50-200 | 20-80 |
| Particle GPU time | 2-4ms | 3-6ms | 2-3ms per eye |
| Overdraw budget | < 2x screen | < 4x screen | < 2x screen |

### Effect Priority System

| Priority | Examples | Budget % | LOD Behavior |
|----------|---------|----------|-------------|
| Critical | Player abilities, UI effects | 40% | Always full quality |
| Important | Nearby combat, environment | 30% | Reduce at medium distance |
| Ambient | Distant effects, atmosphere | 20% | Heavy LOD, remove at distance |
| Polish | Extra sparkles, secondary effects | 10% | First to disable |

---

## CPU vs GPU Particles

### When to Use Each

| Factor | CPU Particles | GPU Particles |
|--------|-------------|---------------|
| Count | < 1,000 per system | 1,000-1,000,000+ |
| Collision | Full physics collision | Limited (depth buffer) |
| Interaction | Read particle state on CPU | Hard to read back |
| Sorting | Easy (for transparency) | Expensive/limited |
| Spawn logic | Complex, conditional | Simple rules |
| Best for | Interactive effects, small bursts | Smoke, snow, ambient |

### GPU Particle Compute Shader

```hlsl
// Particle update compute shader
[numthreads(256, 1, 1)]
void CSMain(uint3 id : SV_DispatchThreadID) {
    Particle p = particleBuffer[id.x];
    
    if (p.lifetime <= 0) return;
    
    // Physics
    p.velocity += gravity * deltaTime;
    p.velocity += windForce(p.position) * deltaTime;
    p.position += p.velocity * deltaTime;
    
    // Lifetime
    p.lifetime -= deltaTime;
    p.age += deltaTime;
    
    // Write back
    particleBuffer[id.x] = p;
}
```

---

## Overdraw Reduction

### The Overdraw Problem
Transparent particles are the #1 performance cost:
- Each overlapping particle requires a blend operation
- 100 overlapping particles = 100x pixel fill cost
- Large particles close to camera are the worst offenders

### Mitigation Strategies

| Strategy | Reduction | Quality Impact |
|----------|----------|---------------|
| Fewer, larger particles | 30-50% | Slight reduction |
| Smaller particles, more spread | 20-40% | More granular look |
| Depth fade (soft particles) | 10-20% | Smoother, fewer artifacts |
| Half-resolution rendering | 50-75% | Slight softness |
| Cut-out (alpha test) | 40-60% | Harder edges |
| Low-res offscreen buffer | 60-80% | Requires upscale |

### Half-Resolution Particle Rendering
1. Render particles to a half-resolution buffer
2. Use depth-aware upscale to composite over scene
3. 4x fewer pixels shaded
4. Slight softness acceptable for smoke/fog/magic

---

## LOD System for Particles

### Distance-Based LOD

| Distance | Particle Count | Sub-Effects | Light | Shadow |
|----------|---------------|-------------|-------|--------|
| Near (< 10m) | 100% | All active | Yes | Yes |
| Medium (10-30m) | 50% | Primary only | Yes | No |
| Far (30-80m) | 25% | Core only | No | No |
| Very far (> 80m) | Billboard or disable | None | No | No |

### Implementation
```csharp
float distanceSqr = (cameraPos - effectPos).sqrMagnitude;
if (distanceSqr > farThresholdSqr) {
    // Disable effect entirely
    system.SetActive(false);
} else if (distanceSqr > medThresholdSqr) {
    // Reduce particles
    emission.rateOverTime = baseRate * 0.25f;
    DisableSubEmitters();
} else if (distanceSqr > nearThresholdSqr) {
    emission.rateOverTime = baseRate * 0.5f;
}
```

---

## Object Pooling

### Pool Architecture

```
ParticlePool
  ├── Fire effects (pool of 10)
  ├── Explosion effects (pool of 5)
  ├── Magic projectiles (pool of 20)
  └── Hit impacts (pool of 30)
```

**Rules:**
- Pre-instantiate effects at level load
- Return to pool when finished (don't destroy)
- If pool exhausted: either skip effect or recycle oldest
- Warm up pools during loading screens
- Track pool hit/miss rates for sizing

### Memory Management
- Share materials across similar effects
- Use texture atlases for particle sprites
- Pre-allocate maximum particle buffers
- Avoid runtime material creation
