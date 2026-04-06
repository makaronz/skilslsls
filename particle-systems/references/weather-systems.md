# Weather Particle Systems

Implement rain, snow, fog, and other atmospheric effects for games and real-time applications.

---

## Rain

### Rain Particle Setup

| Property | Light Rain | Moderate Rain | Heavy Rain |
|----------|-----------|--------------|-----------|
| Particle count | 500-1,000 | 2,000-5,000 | 5,000-15,000 |
| Fall speed | 5-8 m/s | 8-12 m/s | 12-20 m/s |
| Particle shape | Stretched billboard | Stretched billboard | Mesh streak |
| Width | 0.005-0.01m | 0.01-0.02m | 0.02-0.04m |
| Length | 0.3-0.5m | 0.5-1.0m | 1.0-2.0m |
| Color | Light gray, 30% opacity | Gray, 40% opacity | Dark gray, 50% opacity |
| Wind influence | Slight angle (5-10°) | Moderate (10-20°) | Strong (20-40°) |

### Rain Optimization

**Camera-Relative Emission:**
- Emit particles in a box centered on camera
- Box size: 20-40m wide, 10-20m tall
- Particles that leave box are recycled (respawn at top)
- Creates illusion of infinite rain with limited particles

**Screen-Space Rain (Alternative):**
- Render rain as a full-screen post-process
- Multiple layers of scrolling streak textures
- Much cheaper than particles for background rain
- Combine with near-camera particles for foreground

### Rain Interaction

| Surface | Effect | Implementation |
|---------|--------|---------------|
| Ground | Splashes | Sub-emitter on collision, ripple decal |
| Water | Ripples | Animated normal map rings |
| Windows | Streaks | Screen-space drip shader |
| Character | Wetness | Increase roughness, darken albedo |

---

## Snow

### Snow Particle Setup

| Property | Light Snow | Heavy Snow | Blizzard |
|----------|-----------|-----------|---------|
| Particle count | 200-500 | 1,000-3,000 | 3,000-8,000 |
| Fall speed | 0.5-1.5 m/s | 1-3 m/s | 2-5 m/s |
| Horizontal drift | ±0.5 m/s | ±1 m/s | ±3-5 m/s |
| Size | 0.01-0.03m | 0.02-0.05m | 0.03-0.08m |
| Rotation | Slow tumble | Moderate tumble | Fast spin |
| Turbulence | Low | Medium | High |

### Snow Accumulation
- Use runtime height painting on terrain
- Blend snow material based on normal direction (top surfaces)
- Gradual accumulation over time
- Footprint system: depress snow on character/object contact

---

## Fog and Mist

### Implementation Methods

| Method | Quality | Performance | Control |
|--------|---------|------------|---------|
| Distance fog (shader) | Low | Free | Global only |
| Height fog (shader) | Medium | Low | Height-based |
| Volumetric fog (raymarching) | Excellent | Expensive | Full 3D control |
| Particle fog | Good | Medium | Localized |
| Fog volumes (mesh-based) | Good | Medium | Shape-defined |

### Volumetric Fog

```
For each pixel:
  March ray from camera through fog volume
  At each step:
    Sample density (noise + height falloff)
    Sample lighting (shadow map + ambient)
    Accumulate color and opacity
  Blend result with scene
```

**Parameters:**
| Parameter | Effect | Range |
|-----------|--------|-------|
| Density | Thickness | 0.01-1.0 |
| Height falloff | How quickly fog thins with altitude | 0.1-2.0 |
| Noise scale | Wispy variation | 0.01-0.1 |
| Noise speed | Animation | 0.1-1.0 m/s |
| Scattering | Light interaction color | 0.0-1.0 |
| Steps | Quality vs performance | 16-128 |

---

## Wind System

### Global Wind

| Component | Purpose | Implementation |
|-----------|---------|---------------|
| Base direction | Prevailing wind | Vector3 + speed |
| Gusts | Temporal variation | Sine wave + noise |
| Turbulence | Spatial variation | 3D noise field |
| Updrafts | Vertical currents | Height-based force |

### Wind Affecting Particles
```
// Per particle update
float3 windForce = baseWind + gustNoise(time) + turbulenceNoise(position);
velocity += windForce * deltaTime * dragCoefficient;
position += velocity * deltaTime;
```

### Wind Affecting Vegetation
- Vertex displacement in shader
- Use world position as noise input for spatial coherence
- Trunk bends less than branches, branches less than leaves
- Phase offset per branch for desynchronized motion

---

## Day/Night Cycle Integration

| Time | Sky Color | Fog Color | Particle Lighting |
|------|-----------|-----------|------------------|
| Noon | Blue | Light blue/white | Bright white |
| Sunset | Orange-pink | Warm golden | Orange tint |
| Night | Dark blue | Dark blue-gray | Dim blue/moonlight |
| Overcast | Gray | Gray | Flat, diffuse |
| Storm | Dark gray | Dark | Dim, desaturated |
