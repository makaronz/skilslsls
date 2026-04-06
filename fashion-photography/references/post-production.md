# Fashion Post-Production

Professional retouching and color grading workflow for fashion imagery.

---

## Fashion Retouching Workflow

### Step-by-Step Process

| Step | Tool/Technique | Time Estimate |
|------|---------------|---------------|
| 1. RAW Processing | Lightroom: WB, exposure, tone | 2-3 min |
| 2. Cleanup | PS: Healing brush, clone stamp | 5-10 min |
| 3. Skin retouching | PS: Frequency separation, D&B | 15-30 min |
| 4. Body refinement | PS: Liquify (if requested/ethical) | 5-10 min |
| 5. Color grading | PS: Curves, selective color | 5-10 min |
| 6. Hair retouching | PS: Stray hair removal, volume | 5-15 min |
| 7. Garment cleanup | PS: Wrinkle removal, color fix | 5-10 min |
| 8. Final polish | PS: Sharpening, vignette | 2-5 min |

### Skin Retouching Standards

| Level | Description | Use Case | Time |
|-------|-------------|----------|------|
| Light | Remove blemishes only | Catalog, e-commerce | 5-10 min |
| Medium | Even skin tone, reduce under-eye | Editorial, portraits | 15-20 min |
| Heavy | Full frequency separation + D&B | Beauty, cosmetics campaigns | 30-45 min |
| Editorial | Hyper-polished, editorial standard | Magazine covers, luxury | 45-90 min |

---

## Color Grading for Fashion

### Genre-Specific Grades

| Fashion Genre | Color Palette | Contrast | Saturation |
|--------------|--------------|----------|-----------|
| High fashion editorial | Desaturated, teal/orange or monochrome | High | Low-medium |
| Beauty/cosmetics | Neutral, accurate | Medium | Medium (accurate colors) |
| Streetwear | Bold, saturated, high contrast | High | High |
| Bridal | Soft, warm, light and airy | Low-medium | Low-medium |
| Luxury | Rich, deep, warm tones | Medium-high | Medium |
| Minimalist | Clean, neutral, white-dominant | Low | Low |

### Skin Tone Preservation
- Always grade skin tones separately from background
- Use luminosity masks to protect skin from heavy grades
- Check skin tone values: should fall on the skin tone line
- Monitor for unnatural shifts (too green, too magenta, too saturated)

---

## Garment Retouching

### Common Tasks

| Task | Technique | Priority |
|------|-----------|---------|
| Wrinkle removal | Clone stamp + liquify | High |
| Color correction | HSL + selective color | High (match physical item) |
| Fabric texture enhancement | High-pass sharpening with mask | Medium |
| Stray threads removal | Healing brush | Medium |
| Fit adjustments | Liquify (subtle only) | If requested |
| Pattern alignment | Warp tool at seams | Low (editorial) |

### Color Accuracy
1. Include ColorChecker in reference shot
2. Create camera profile from reference
3. Match garment color on calibrated monitor
4. Check against physical sample
5. Output in sRGB for web (accurate for screens)

---

## Compositing for Fashion

### Background Replacement
1. Extract subject with Pen Tool + Refine Edge
2. Place on new background
3. Match lighting direction and color temperature
4. Add cast shadow for grounding
5. Apply consistent color grade to all layers
6. Add subtle edge glow for integration

### Multi-Image Composite
- Use same camera position and focal length
- Match lighting setup across all captures
- Composite in order: background → main subject → foreground
- Blend modes: use Normal for subjects, Multiply for shadows
- Group related layers for organized file structure

---

## Delivery Formats

| Deliverable | Format | Resolution | Notes |
|------------|--------|-----------|-------|
| Magazine print | TIFF, Adobe RGB, 300 DPI | Full resolution | CMYK conversion by publisher |
| Lookbook digital | JPEG 90%, sRGB | 3000px long | High quality for zoom |
| Social media | JPEG 85%, sRGB | Platform-specific | Optimized file size |
| Billboard/large format | TIFF, Adobe RGB | Full resolution | Will be upscaled |
| Website/e-commerce | JPEG 80-85%, sRGB | 2000-2500px | Balance quality and speed |
| Campaign press kit | TIFF + JPEG, sRGB | Full + web sizes | Both print and digital ready |
