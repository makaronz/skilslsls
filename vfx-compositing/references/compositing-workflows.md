# VFX Compositing Workflows

Node-based compositing pipelines for professional visual effects production.

---

## Compositing Order

Standard composite script flows:
```
Background Plate → Grade/Color → Set Extension → CG Element Integration
  → Green Screen Foreground → Roto/Paint Fixes → Final Grade
  → Lens Effects (grain, vignette, distortion) → Output
```

---

## CG Integration Pipeline

### Render Passes

| Pass | Content | Compositing Use |
|------|---------|----------------|
| Beauty | Final rendered image | Starting point |
| Diffuse | Surface color without specular | Color correction base |
| Specular | Reflective highlights | Independent highlight control |
| Shadow | Shadow contribution | Adjust shadow density |
| AO | Contact shadows | Multiply for depth |
| Z-Depth | Distance from camera | DOF, fog |
| Normal | Surface direction | Relighting |
| Motion Vector | Pixel movement | Motion blur |
| Cryptomatte | Object/material IDs | Easy selection masking |

### Rebuild Formula
```
Final = (Diffuse * Color + Specular + Reflection + Emission) * AO * Shadow
```

---

## Plate Cleanup

| Task | Tool | Technique |
|------|------|-----------|
| Wire removal | RotoPaint + Tracker | Track point, paint out per frame |
| Marker removal | Clone + FrameHold | Paint from clean frame, track |
| Rig removal | Roto + clean plate | Mask area, replace with plate |

### Stabilize-Paint-Destabilize
1. Track area to be cleaned
2. Stabilize plate (apply inverse track)
3. Paint on stabilized frame
4. Destabilize (re-apply tracking)
5. Clean paint moves with original motion

---

## Shot Finishing

### Lens Effects
| Effect | Purpose | Implementation |
|--------|---------|---------------|
| Film grain | Match original footage | Grain node with scanned grain |
| Lens distortion | Match plate | STMap or LensDistortion |
| Chromatic aberration | Realism | Channel offset (R, G, B) |
| Vignette | Edge darkening | Radial gradient multiply |
| Depth of field | Focus simulation | ZDefocus with depth pass |
| Bloom/glow | Bright area spread | Exponential glow on highlights |

### Color Pipeline
- Work in linear color space (scene-referred)
- Apply ACES or custom color management
- View through display transform
- Never grade in display space

---

## Node-Based Best Practices

### Nuke Script Organization
- Color-code nodes by function (blue=color, green=keying, red=roto)
- Use Backdrop nodes to group related operations
- Label every critical node with descriptive names
- Use dot nodes for clean pipe routing
- Maintain left-to-right or top-to-bottom flow
- Add Viewer nodes at key checkpoints

### Performance
| Technique | Benefit |
|-----------|---------|
| Proxy workflow | 2-4x faster during development |
| Concatenated transforms | Reduce interpolation artifacts |
| Bbox optimization | Process only needed pixels |
| Disk caching | Faster playback of complex trees |

---

## Deliverables

| Output | Format | Color Space | Bit Depth |
|--------|--------|-------------|-----------|
| VFX comp to editorial | EXR or DPX | ACEScg or log | 16-bit half |
| Final delivery | DPX sequence | Per facility spec | 10-bit log |
| Web/streaming | ProRes or H.264 | Rec.709 | 8-10 bit |
| Archive | EXR | ACEScg | 16-bit half |
