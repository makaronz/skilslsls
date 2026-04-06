# Magic and Energy Effects

Design stylized particle effects for magic spells, energy weapons, shields, and supernatural phenomena.

---

## Effect Design Framework

### Magic Effect Components

Most magic effects combine these layers:

| Layer | Purpose | Technique |
|-------|---------|-----------|
| Core | Bright center of energy | Additive sprite, glow |
| Trails | Motion and flow | Ribbon/trail renderer |
| Particles | Sparkle and detail | Billboard sprites |
| Distortion | Energy warping space | Screen-space distortion |
| Light | Illumination of scene | Dynamic point/spot light |
| Sound | Audio feedback | Synced to visual phases |

---

## Common Magic Effects

### Magic Projectile

**Structure:**
1. **Leading edge**: Bright core sprite (additive, 2-3x glow)
2. **Trail**: Ribbon renderer following path (fade out over 0.3-1s)
3. **Particles**: Small sparkles shed along trail
4. **Distortion**: Subtle heat haze around core

**Trail Renderer Settings:**
| Property | Value |
|----------|-------|
| Width curve | Start 0.5m → end 0.05m |
| Color | Bright → transparent (match element) |
| Lifetime | 0.3-1.0 seconds |
| Min vertex distance | 0.1m (smooth trail) |
| Texture mode | Stretch or Tile |
| Material | Additive, soft trail texture |

### Shield / Barrier

| Property | Settings |
|----------|---------|
| Shape | Sphere mesh or hemisphere |
| Shader | Fresnel edge glow + noise pattern |
| Hit reaction | Ripple from impact point |
| Particles | Slow-moving energy motes on surface |
| Animation | Noise-driven opacity and UV scrolling |

**Fresnel Shield Shader Approach:**
```hlsl
float fresnel = pow(1.0 - dot(viewDir, normal), fresnelPower);
float pattern = tex2D(noiseTexture, uv + time * scrollSpeed).r;
float alpha = fresnel * pattern * intensity;
color = shieldColor * alpha;
```

### Healing / Buff Aura

- Ring of particles rising around character
- Soft upward spiral motion
- Green/gold/white color scheme
- Cross-shaped or leaf-shaped particles
- Subtle body glow (post-process or additive overlay)
- Duration: match buff duration, gentle fade in/out

### Lightning / Electric

| Component | Implementation |
|-----------|---------------|
| Main bolt | Segmented line with random offsets (regenerate per frame) |
| Branches | Shorter, dimmer copies branching from main bolt |
| Glow | Additive bloom around bolt segments |
| Sparks | Burst particles at impact/branch points |
| Sound | Crackle synced to bolt generation |

**Bolt Generation:**
1. Define start and end points
2. Find midpoint, offset perpendicular by random amount
3. Recursively subdivide (4-6 levels)
4. Draw line segments with width based on depth
5. Regenerate offsets every 1-3 frames for flickering

---

## Element Color Guides

| Element | Core Color | Trail Color | Glow Color |
|---------|-----------|-------------|-----------|
| Fire | White-yellow | Orange-red | Warm orange |
| Ice | White-cyan | Light blue | Cool blue |
| Lightning | White | Purple-blue | Bright purple |
| Nature | White-green | Emerald | Soft green |
| Dark/Shadow | Dark purple | Black-purple | Deep violet |
| Holy/Light | White | Gold-white | Warm gold |
| Arcane | White-pink | Magenta | Pink-purple |
| Water | White-blue | Teal | Aqua |

---

## Performance Tips

- Pre-warm effects: Simulate particles before showing
- Use object pooling for frequently spawned effects
- LOD: Simplify effects at distance (remove sub-emitters, reduce count)
- Limit active effects: Queue or cull if too many on screen
- Use sprite atlases for all particle textures
- Bake complex effects to flipbook animations for mobile
