# Photoshop Retouching Techniques

Advanced retouching and compositing techniques for professional photo editing.

---

## Essential Retouching Tools

### Healing and Cloning

| Tool | Use Case | Settings |
|------|----------|---------|
| Spot Healing Brush | Quick blemish removal | Content-Aware, sample all layers |
| Healing Brush | Controlled source sampling | Set source point with Alt/Option-click |
| Clone Stamp | Precise pattern/texture work | Adjust opacity, flow, hardness |
| Content-Aware Fill | Large area removal | Select area, Edit → Content-Aware Fill |
| Patch Tool | Drag to replace area | Content-Aware mode for best results |

### Selection Techniques

| Method | Best For | Precision |
|--------|----------|----------|
| Quick Selection | Clear edges, contrasting subjects | Good |
| Select Subject (AI) | People, animals, objects | Very good |
| Pen Tool | Hard edges, products, architecture | Perfect |
| Color Range | Selecting by color (sky, clothing) | Good |
| Focus Area | Selecting by focus depth | Moderate |
| Channel-based | Complex edges (hair, trees) | Excellent |
| Select and Mask | Refining any selection | Excellent |

---

## Frequency Separation

### Setup
1. Duplicate background layer twice → name "Low" and "High"
2. Hide High layer, select Low layer
3. Apply Gaussian Blur: 8-12px for portraits (larger for full body)
4. Select High layer, make visible
5. Image → Apply Image: Source = Low layer, Blending = Subtract, Scale = 2, Offset = 128
6. Set High layer blending mode to Linear Light

### Editing
| Layer | Edit With | Purpose |
|-------|-----------|---------|
| Low frequency | Soft brush, mixer brush | Even skin tones, smooth color transitions |
| High frequency | Clone stamp, healing brush | Remove texture blemishes, keep skin detail |

---

## Dodge and Burn

### Setup
- Create new layer, fill with 50% gray
- Set blending mode to Soft Light
- Name "Dodge and Burn"

### Technique
| Action | Brush | Opacity | Purpose |
|--------|-------|---------|---------|
| Dodge (brighten) | White, soft | 3-5% | Highlight cheekbones, nose bridge, chin |
| Burn (darken) | Black, soft | 3-5% | Deepen jawline, contour, shadows |
| Even tones | White on dark spots, black on bright spots | 3-5% | Smooth skin tone variations |

### Areas to Target
- Under eyes (lighten bags)
- Jawline (define with shadow)
- Cheekbones (highlight)
- Forehead (even tones)
- Nose (slim with shadow sides)
- Neck (even with face tone)

---

## Color Grading

### Curves Color Grading
| Channel | Highlights | Shadows | Effect |
|---------|-----------|---------|--------|
| Red | Up | Down | Warm highlights, cool shadows |
| Green | Down | Up | Magenta highlights, green shadows |
| Blue | Up | Down | Cool highlights, warm (yellow) shadows |

### Selective Color Adjustment
- Target specific color ranges without affecting others
- Adjust CMYK sliders within each color channel
- Excellent for skin tone refinement (adjust Reds and Yellows)

### Color Lookup Tables (LUTs)
- Apply cinematic color grades quickly
- Available as .cube or .3dl files
- Adjustment Layer → Color Lookup
- Reduce opacity for subtlety (30-60%)
- Create custom LUTs from your favorite grade

---

## Compositing Essentials

### Layer Blend Modes

| Mode | Use Case | Effect |
|------|----------|--------|
| Normal | Standard layering | Full replacement |
| Multiply | Darken, add shadows | Multiplies luminance values |
| Screen | Lighten, add glow | Lightens without blowing out |
| Overlay | Contrast, color grade | Darkens darks, lightens lights |
| Soft Light | Subtle contrast, D&B | Gentle version of Overlay |
| Color | Apply color only | Preserves luminance |
| Luminosity | Apply brightness only | Preserves color |

### Masking Best Practices
- Always use layer masks (non-destructive)
- Paint with black to hide, white to reveal
- Use feathered brushes for soft transitions
- Adjust mask density and feather in Properties panel
- Use "Apply Mask" only when finalizing
