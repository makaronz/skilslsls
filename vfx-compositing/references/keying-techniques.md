# Keying Techniques for VFX Compositing

Extract clean mattes from green/blue screen footage using professional keying workflows.

---

## Screen Color Selection

| Color | When to Use | Avoid When |
|-------|------------|-----------|
| Green | Digital cameras (cleanest channel), most situations | Subject has green clothing/props |
| Blue | Film cameras, subjects with green elements | Blonde hair (similar luminance) |

## On-Set Requirements

| Factor | Standard | Optimal |
|--------|---------|---------|
| Screen evenness | +/-0.5 stop variation | +/-0.3 stop variation |
| Subject-screen distance | 6+ feet | 10+ feet (reduce spill) |
| Lighting ratio | Screen slightly brighter | 0.5-1 stop above subject key |

---

## Keying Tools

### Nuke Keyers

| Keyer | Strength | Best For |
|-------|----------|---------|
| Keylight | Fast, good first pass | Well-lit, even screens |
| Primatte | Complex edges | Hair, smoke, motion blur |
| IBKGyre | Handles uneven screens | Difficult footage |
| Difference key | Simple, fast | Clean plates available |

---

## Multi-Pass Keying Workflow

### Step 1: Core Matte
- Apply primary keyer (Keylight or Primatte)
- Pull clean core matte focusing on solid body areas
- Solid white interior, solid black exterior
- Don't worry about edges yet

### Step 2: Edge Matte
- Duplicate or add second keyer with softer settings
- Preserve hair detail, transparency, and motion blur
- Allow some noise in edges (will clean up)

### Step 3: Combine
- Use core matte for body, edge matte for boundary/hair
- Combine with maximum/screen operation
- Edge extend to fill dark boundary pixels

### Step 4: Spill Suppression
- Remove color contamination from screen reflection
- Replace affected channel: G channel with average of R and B
- Fine-tune to avoid desaturating legitimate greens in subject

### Step 5: Edge Treatment
| Technique | Purpose | Settings |
|-----------|---------|---------|
| Edge blur | Soften hard matte edges | 0.5-1.5 pixels |
| Edge erode | Remove color fringe | 0.5-1 pixel |
| Edge extend | Push foreground color into edges | 2-4 pixels |
| Light wrap | Blend BG light into subject edges | Subtle, 5-10% opacity |

---

## Handling Difficult Footage

### Motion Blur
- Wider keyer tolerance needed
- Maintain pre-multiplied workflow
- Accept softer matte in motion areas
- Use temporal smoothing for stability

### Uneven Green Screen
- Pre-grade screen to more uniform color before keying
- Use garbage matte to isolate best screen area
- IBKGyre excels at uneven illumination
- Multiple keyers for different screen regions

### Fine Hair Detail
- Dedicated edge keyer (Primatte excellent for hair)
- Avoid over-eroding edges
- Light wrap helps integrate wispy edges
- Use despill carefully around hair edges

### Transparent/Reflective Objects
- Shoot clean plate (background without subject)
- Use difference key for glass/water elements
- Additive composite for transparent elements

---

## Quality Checks

| Check | Method | Pass Criteria |
|-------|--------|---------------|
| Over white BG | Composite on white | No dark fringing |
| Over black BG | Composite on black | No light fringing |
| Over color BG | Red/green/blue | No spill visible |
| Alpha channel | Direct view | Clean edges, no holes |
| 200% zoom | Edge inspection | Smooth, natural transition |
| Real-time playback | Temporal check | No flickering or chatter |
