# Color Grading for VFX

Apply consistent color grades across VFX shots and match composited elements to plates.

---

## Color Management

### ACES Pipeline

| Component | Purpose |
|-----------|---------|
| ACEScg | Working space for CG and compositing |
| ACEScc | Log space for grading |
| IDT | Converts camera footage to ACES |
| ODT | Converts ACES to display format |

### Working Spaces

| Space | Use For | Operations |
|-------|---------|-----------|
| Linear | Compositing, CG integration | Merge, blur, lighting |
| Log | Color grading, final look | Curves, color wheels |
| sRGB/Rec.709 | Final output only | Delivery |

**Rule:** Composite in linear, grade in log, deliver in display.

---

## Shot Matching

### Matching CG to Plate

| Element | Method |
|---------|--------|
| Exposure | Histogram comparison, match brightness |
| Contrast | Match shadow/highlight ratio |
| Color temperature | Use neutral references |
| Saturation | Match vibrancy level |
| Black point | Match deepest shadow value |

### Shot-to-Shot Consistency
1. Choose hero shot as reference grade
2. Apply base grade to reference
3. Match each subsequent shot to reference
4. Fine-tune skin tones and key elements

---

## Grading Tools

### Nuke Color Nodes

| Node | Purpose | Use |
|------|---------|-----|
| Grade | Lift/Gain/Multiply/Offset | Primary correction |
| ColorCorrect | Shadows/Mids/Highlights | Three-way balance |
| HueShift | Rotate hues | Palette shift |
| Saturation | Colorfulness | Boost or reduce |
| Exposure | EV-based brightness | Match exposure levels |

---

## Common VFX Color Challenges

| Challenge | Solution |
|-----------|---------|
| CG too clean | Add noise, micro-variation, imperfections |
| CG too saturated | Desaturate to match plate |
| Green spill on subject | Despill before grading |
| Mismatched blacks | Grade node to set matching black point |
| CG lacks atmosphere | Depth-based fog/haze |
| Different cameras | Normalize all to common color space |

---

## LUT Workflows

### LUT Types
| Type | Size | Use |
|------|------|-----|
| 1D LUT | 1024 entries | Simple gamma/contrast |
| 3D LUT (33^3) | 33x33x33 | Full color transform |

**Never bake LUT into comp** — keep as viewing transform only.

---

## Deliverables

| Output | Format | Color Space | Depth |
|--------|--------|-------------|-------|
| Comp to editorial | EXR/DPX | ACEScg/log | 16-bit |
| Final grade | DPX | Per facility | 10-bit |
| Web delivery | ProRes/H.264 | Rec.709 | 8-10 bit |
| HDR | EXR | Rec.2020 PQ | 10-12 bit |
