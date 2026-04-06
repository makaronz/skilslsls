# Lightroom Editing Guide

Master Adobe Lightroom workflows for efficient, non-destructive photo editing.

---

## Develop Module Workflow

### Recommended Edit Order

| Step | Panel | Key Adjustments |
|------|-------|----------------|
| 1 | Profile | Choose camera profile (Adobe Color, Adobe Landscape, etc.) |
| 2 | White Balance | Set correct WB using eyedropper or sliders |
| 3 | Exposure | Set overall brightness for key subject |
| 4 | Tone | Highlights, Shadows, Whites, Blacks |
| 5 | Presence | Texture, Clarity, Dehaze |
| 6 | Vibrance/Saturation | Color intensity (Vibrance first) |
| 7 | Tone Curve | Fine-tune contrast and tonal response |
| 8 | HSL | Targeted color adjustments |
| 9 | Color Grading | Creative color toning (shadows/mids/highlights) |
| 10 | Detail | Sharpening and noise reduction |
| 11 | Lens Corrections | Enable profile, remove chromatic aberration |
| 12 | Transform | Straighten horizons, correct perspective |
| 13 | Local Adjustments | Graduated filter, radial filter, brush |
| 14 | Crop | Final composition |

---

## Masking Tools

### AI-Powered Masks (LR 2023+)

| Mask Type | Use Case | Refinement |
|-----------|----------|-----------|
| Select Subject | Isolate main subject from background | Add/subtract brush |
| Select Sky | Target sky separately | Refine edge with feather |
| Select Background | Everything except subject | Invert subject mask |
| Select People | Face, body, hair, clothes | Component selection |
| Brush | Manual painting | Flow/density for control |
| Linear Gradient | Graduated effect (sky, ground) | Adjust angle and spread |
| Radial Gradient | Vignette or spotlight effect | Feather for soft edge |

### Mask Intersections
- Combine multiple masks with Add/Subtract/Intersect
- Example: Select Sky → Intersect with Gradient = upper portion of sky only
- Powerful for targeted adjustments without manual brushing

---

## Tone Curve Techniques

### Parametric vs Point Curve

| Mode | Control | Best For |
|------|---------|----------|
| Parametric | Slider-based zones | Quick, safe adjustments |
| Point curve | Click and drag | Precise, creative control |

### Common Curve Shapes

| Curve Shape | Effect | Use Case |
|-------------|--------|----------|
| S-curve (gentle) | Increased contrast | Standard enhancement |
| Lifted blacks | Faded, matte look | Film/vintage aesthetic |
| Crushed highlights | Darker, moody ceiling | Dark and moody edit |
| RGB channel curves | Color grading | Teal shadows, warm highlights |

---

## Presets

### Building Effective Presets

**What to Include:**
- Tone curve settings
- HSL adjustments
- Color grading
- Calibration
- Sharpening and NR defaults

**What to Exclude:**
- Exposure (varies per image)
- White balance (varies per image)
- Crop (varies per image)
- Spot removal
- Local adjustments

### Preset Organization
- Group by style: Natural, Moody, Film, B&W, Bright & Airy
- Group by genre: Portrait, Landscape, Street, Wedding
- Name descriptively: "Warm Film — High Contrast"

---

## Performance Optimization

| Setting | Recommendation | Impact |
|---------|---------------|--------|
| Smart Previews | Generate on import | Faster editing, offline work |
| Preview size | 1:1 on import | Faster zoom |
| Camera Raw cache | 20-50 GB | Faster develop module |
| GPU acceleration | Enable | Faster image rendering |
| Catalog location | SSD | Faster overall performance |
| Catalog size | < 100K images ideal | Maintain responsiveness |

---

## Export Presets

| Use Case | Format | Quality | Resize | Sharpen | Color Space |
|----------|--------|---------|--------|---------|-------------|
| Web/social | JPEG | 80-85% | 2048px long | Screen, standard | sRGB |
| Print (lab) | JPEG | 100% | No resize | Matte/glossy, standard | sRGB |
| Client delivery | JPEG | 90-95% | No resize | Screen, low | sRGB |
| Archive | TIFF or DNG | Max | No resize | None | ProPhoto RGB |
| Portfolio | JPEG | 90% | 3000px long | Screen, standard | sRGB |
