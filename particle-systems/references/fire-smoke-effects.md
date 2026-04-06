# Fire and Smoke Effects

Create realistic fire, smoke, and explosion particle effects for real-time applications.

---

## Fire Effects

### Campfire / Torch

| Property | Value | Notes |
|----------|-------|-------|
| Emitter shape | Cone (15-30°) | Narrow for torch, wider for campfire |
| Particle count | 50-200 | CPU-friendly range |
| Lifetime | 0.5-1.5 seconds | Short for flicker |
| Start size | 0.1-0.3m | Small at base |
| End size | 0.5-1.5m | Expand as they rise |
| Start color | White-yellow (#FFFFAA) | Hottest at base |
| End color | Orange-red (#FF4400) → transparent | Cool as particles rise |
| Velocity | 1-3 m/s upward | Gentle rise |
| Turbulence | Medium | Flickering motion |
| Blend mode | Additive | Bright, glowing |
| Texture | Soft circle or fire sprite sheet | Animated UVs for variety |

**Layered Approach:**
1. **Core flames**: Small, bright, white-yellow, additive
2. **Outer flames**: Larger, orange-red, soft-additive
3. **Embers**: Tiny, bright points rising with turbulence
4. **Heat distortion**: Screen-space distortion (post-process)
5. **Light source**: Point light matching flame color, flickering intensity

### Explosion

**Phases:**
| Phase | Duration | Elements |
|-------|----------|---------|
| Flash | 0-0.1s | Bright white sphere, screen shake |
| Fireball | 0.1-0.5s | Expanding fire sprites, debris launch |
| Smoke | 0.3-3.0s | Dark smoke billowing outward |
| Aftermath | 1-10s | Lingering smoke, embers, dust |

**Fireball Settings:**
- Burst emission: 500-2000 particles in single frame
- Spherical emission with high initial velocity (10-50 m/s)
- Rapid size increase over lifetime
- Color: white → yellow → orange → dark gray
- Add gravity drag to slow expansion
- Sub-emitters for secondary sparks and debris

---

## Smoke Effects

### Smoke Characteristics

| Smoke Type | Color | Density | Rise Speed | Turbulence |
|-----------|-------|---------|-----------|------------|
| Clean burn | Light gray | Low | Fast (2-5 m/s) | Low |
| Dirty burn | Dark gray/black | High | Medium (1-3 m/s) | Medium |
| Steam | White, transparent | Very low | Fast | Low |
| Dust | Brown/tan | Medium | Slow (0.5-1 m/s) | High |
| Fog (ground) | White/gray | Low | Near zero | Very low |

### Billboard vs Volume Rendering

| Method | Quality | Performance | Best For |
|--------|---------|------------|----------|
| Billboard sprites | Medium | Fast | Most game smoke |
| Flipbook animation | Good | Fast | Stylized smoke |
| Flowmap animation | Very good | Medium | Close-up smoke |
| Raymarched volumes | Excellent | Expensive | Cinematics, hero shots |
| Vector field driven | Very good | Medium | Smoke following paths |

### Smoke Tips
- Use soft particles (depth fade) to avoid hard intersections with geometry
- Sort particles back-to-front for correct alpha blending
- Add subtle wind influence for outdoor smoke
- Vary particle rotation speed for natural look
- Use noise-based opacity for wispy edges
- Layer 2-3 particle sizes for depth

---

## Performance Optimization

### Particle Count Guidelines

| Effect | Budget (Mobile) | Budget (Desktop) | Budget (Console) |
|--------|----------------|------------------|------------------|
| Campfire | 30-80 | 100-300 | 150-400 |
| Torch | 15-40 | 50-150 | 75-200 |
| Explosion | 100-300 | 500-2000 | 1000-3000 |
| Ambient dust | 20-50 | 50-200 | 100-300 |
| Smoke trail | 20-60 | 50-200 | 100-300 |

### Optimization Techniques
- Use GPU particles for >500 particle effects
- Pool and reuse particle systems (don't create/destroy)
- LOD: Reduce particle count and disable sub-effects at distance
- Use sprite sheets instead of separate textures
- Reduce overdraw: smaller particles, less overlap
- Disable shadows on particles unless critical
- Use mesh particles instead of billboards for debris
