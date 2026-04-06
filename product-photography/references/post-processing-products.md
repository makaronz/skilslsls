# Product Post-Processing

Professional retouching and editing workflows for product photography.

---

## Background Removal and Cleanup

### Pure White Background

**Photoshop Workflow:**
1. Select subject (Select → Subject or Pen Tool for precision)
2. Refine Edge (Select and Mask for fine edges)
3. Create white layer beneath
4. Paint transitions with soft brush
5. Verify: Threshold adjustment → should be no gray spots

**Threshold Test:**
- Apply Threshold adjustment temporarily (level ~250)
- Any non-white areas will appear black
- Fix areas that should be white
- Remove threshold when done

### Background Alternatives

| Background | Technique | Use Case |
|-----------|-----------|----------|
| Pure white | Bright field + PS cleanup | Amazon, most e-commerce |
| Gradient gray | Radial gradient overlay | Premium/luxury products |
| Solid color | Color fill layer | Brand-specific stores |
| Shadow on white | Keep natural shadow | Grounded appearance |
| Transparent (PNG) | Subject extraction | Compositing flexibility |

---

## Color Correction

### Achieving Color Accuracy

| Step | Tool | Purpose |
|------|------|---------|
| White balance | Eyedropper on gray card | Remove color cast |
| Levels/Curves | RGB channels | Match product color |
| HSL adjustment | Targeted color shifts | Fine-tune specific colors |
| Color checker | X-Rite profile | Scientific accuracy |

### Color Matching Workflow
1. Include X-Rite ColorChecker in reference shot
2. Create camera profile from reference
3. Apply profile to all images in batch
4. Fine-tune individual products if needed
5. Compare on calibrated monitor vs physical product
6. Export in sRGB for web (screen display standard)

---

## Retouching

### Common Product Retouching Tasks

| Task | Tool | Technique |
|------|------|-----------|
| Dust removal | Healing Brush / Clone Stamp | Sample nearby clean area |
| Scratch removal | Healing Brush | Follow surface texture |
| Label straightening | Warp / Liquify | Align text and graphics |
| Reflection cleanup | Clone Stamp | Match surrounding reflection |
| Surface smoothing | Frequency Separation | Separate texture from color |
| Wrinkle removal (fabric) | Liquify | Push/smooth fabric |

### Frequency Separation for Products
1. Duplicate layer twice
2. Low frequency: Gaussian blur (radius 5-10px)
3. High frequency: Apply Image (subtract low from original)
4. Edit low layer for color/tone (smooth transitions)
5. Edit high layer for texture (remove scratches, dust)

---

## Batch Processing

### Lightroom Batch Workflow
1. Edit one representative image fully
2. Copy settings (Ctrl/Cmd + Shift + C)
3. Select all similar images
4. Paste settings (Ctrl/Cmd + Shift + V)
5. Quick review: adjust individual images as needed
6. Export with preset (format, size, naming)

### Photoshop Actions for Products
- Create action for common tasks:
  - Resize to platform dimensions
  - Add white background layer
  - Apply sharpening for web
  - Convert to sRGB
  - Save as JPEG with quality setting

### Export Settings

| Platform | Format | Quality | Resolution | Color Space |
|----------|--------|---------|-----------|-------------|
| Amazon | JPEG | 85-95% | 2000×2000px | sRGB |
| Shopify | JPEG/WebP | 80-90% | 2048×2048px | sRGB |
| Print catalog | TIFF | Uncompressed | 300 DPI | Adobe RGB/CMYK |
| Social media | JPEG | 80-85% | Platform-specific | sRGB |
| Wholesale/B2B | JPEG/PNG | 90%+ | 3000×3000px | sRGB |
