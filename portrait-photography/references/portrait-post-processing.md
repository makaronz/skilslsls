# Portrait Post-Processing

Professional retouching workflow for natural, polished portrait images.

---

## Lightroom Workflow

### Import and Culling
1. Import with standard metadata preset
2. First pass: Flag picks (P) and rejects (X)
3. Second pass: Rate picks 1-5 stars
4. Color label for specific edits needed

### Global Adjustments

| Adjustment | Portrait Approach |
|-----------|-------------------|
| White Balance | Warm slightly (+200-500K for warmth) |
| Exposure | Correct for face brightness |
| Contrast | Moderate (+10 to +25) |
| Highlights | Pull back (-20 to -50) to recover skin |
| Shadows | Open slightly (+10 to +30) for shadow detail |
| Whites/Blacks | Set for full tonal range |
| Clarity | Low to moderate (-10 to +15) for skin |
| Vibrance | Slight boost (+10 to +20) |
| Saturation | Careful — avoid orange skin (+0 to +5) |

### HSL for Skin Tones
| Channel | Adjustment | Purpose |
|---------|-----------|---------|
| Orange Hue | Shift slightly right (+5) | More natural skin |
| Orange Saturation | Reduce slightly (-10 to -20) | Less orange cast |
| Orange Luminance | Increase (+10 to +20) | Brighter, cleaner skin |
| Red Saturation | Reduce (-10 to -15) | Reduce blotchiness |
| Yellow Luminance | Slight increase | Skin warmth |

---

## Photoshop Retouching

### Non-Destructive Workflow
1. Duplicate background layer
2. All retouching on new layers (non-destructive)
3. Use adjustment layers with masks
4. Save as PSD with layers for future editing
5. Flatten only for final export

### Skin Retouching (Natural Look)

**Frequency Separation:**
1. Duplicate layer twice
2. Low: Gaussian Blur (radius 8-12px for portraits)
3. High: Apply Image → subtract low from original
4. Edit low layer: Even skin tones with soft brush
5. Edit high layer: Remove blemishes while keeping texture

**Dodge and Burn:**
- Create new layer, fill 50% gray, set to Soft Light blend
- Paint with white (3-5% opacity) to brighten
- Paint with black (3-5% opacity) to deepen shadows
- Even out skin tones, enhance facial structure
- Subtle application — should be invisible

### What to Retouch vs What to Keep

| Remove | Keep |
|--------|------|
| Temporary blemishes (pimples) | Freckles |
| Under-eye bags (reduce, not remove) | Moles (unless requested) |
| Stray hairs | Natural skin texture |
| Clothing wrinkles (major) | Laugh lines (reduce if desired) |
| Background distractions | Scars (ask client preference) |

---

## Eye Enhancement
1. Brighten whites slightly (dodge, not pure white)
2. Enhance iris with gentle contrast boost
3. Sharpen eyes with subtle Unsharp Mask
4. Ensure catchlight is present and bright
5. Subtle — eyes should look natural, not alien

## Teeth Whitening
1. Select teeth with lasso tool (feathered)
2. Hue/Saturation → select Yellows → reduce saturation (-30 to -50)
3. Increase lightness slightly (+5 to +15)
4. Subtle — teeth should look natural, not bleached

---

## Export Settings for Portraits

| Output | Format | Resolution | Color Space | Sharpening |
|--------|--------|-----------|-------------|-----------|
| Web gallery | JPEG 80-85% | 2048px long | sRGB | Screen sharpen |
| Social media | JPEG 80% | 1080-1200px | sRGB | Screen sharpen |
| Client proofing | JPEG 90% | 3000px long | sRGB | Low sharpen |
| Print (lab) | JPEG 100% or TIFF | Full resolution | sRGB or Adobe RGB | Matte/glossy sharpen |
| Archive | PSD or TIFF | Full resolution | ProPhoto RGB | None (sharpen on export) |
