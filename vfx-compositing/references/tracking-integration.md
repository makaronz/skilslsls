# Tracking and 3D Integration

Match-move camera and objects for seamless VFX integration with live-action footage.

---

## 2D Tracking

### Point Tracking Types

| Tracker Type | Points | Output | Use Case |
|-------------|--------|--------|----------|
| 1-point | 1 | Translation (x, y) | Stabilize, simple follow |
| 2-point | 2 | Translation + rotation + scale | Logo, simple match |
| 4-point corner pin | 4 | Perspective transform | Screen replacement |
| Planar (Mocha) | Surface | Full perspective warp | Complex surfaces |

### Best Practices
- Choose high-contrast, unique features as track points
- Search region should be 2-3x pattern size
- Check tracks by playing back — watch for slipping
- Manual keyframe corrections where auto-tracking fails

---

## 3D Camera Tracking

### Solve Process
1. Feature detection across all frames
2. Feature matching between frames
3. Camera path computation
4. Iterative refinement
5. Coordinate system setup (ground plane, scale)

### Software Comparison

| Software | Quality | Cost | Notes |
|----------|---------|------|-------|
| SynthEyes | Excellent | $599 | Industry matchmove standard |
| PFTrack | Excellent | $$$$ | Full tracking suite |
| 3DEqualizer | Excellent | $$$$ | Major studio standard |
| Nuke CameraTracker | Good | Included | Quick solves |
| Blender | Good | Free | Rapidly improving |

### Quality Metrics

| Metric | Good | Acceptable | Redo |
|--------|------|-----------|------|
| Solve error | < 0.3px | 0.3-0.8px | > 1.0px |
| Tracked points | 100+ | 50+ | < 30 |
| Frame coverage | Full frame | Mostly covered | Clustered |

---

## Object Tracking

| Track Type | Use Case | Method |
|-----------|----------|--------|
| Rigid body | Car, phone | Point track + solve orientation |
| Planar surface | Screen, wall | Mocha planar tracker |
| Deforming | Face, cloth | Mesh tracker or mocap |

### Screen Replacement Pipeline
1. Track 4 corners of screen in footage
2. Corner pin replacement content
3. Match screen reflections and lighting
4. Add subtle glow and edge blend
5. Color match to ambient lighting
6. Add motion blur matching plate

---

## Set Extension Workflow

### Camera Projection
1. Solve camera from plate
2. Paint matte painting matching camera angle
3. Project painting onto 3D geometry from camera position
4. Camera movement creates depth parallax
5. Multiple projections for different depth planes

### Integration Checklist
- [ ] Camera solve error below 0.5px
- [ ] Ground plane correctly set
- [ ] Scale matches real-world measurements
- [ ] CG sits correctly on tracked surfaces
- [ ] Shadow direction matches plate lighting
- [ ] Color temperature matches plate
- [ ] Motion blur matches shutter angle
- [ ] Atmospheric haze applied by depth
- [ ] Film grain matches plate characteristics
