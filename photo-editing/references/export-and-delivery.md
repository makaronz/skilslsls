# Export and Delivery Guide

Prepare and deliver edited photos for web, print, and client delivery.

---

## File Formats

### Format Comparison

| Format | Compression | Quality | Transparency | Best For |
|--------|------------|---------|-------------|----------|
| JPEG | Lossy | Good-Excellent | No | Web, social, client delivery |
| PNG | Lossless | Excellent | Yes | Graphics, logos, transparency |
| TIFF | Lossless/LZW | Maximum | Yes | Print, archive, compositing |
| WebP | Lossy/Lossless | Excellent | Yes | Modern web (30% smaller than JPEG) |
| AVIF | Lossy/Lossless | Excellent | Yes | Next-gen web (50% smaller than JPEG) |
| PSD | Uncompressed | Maximum | Yes | Working files with layers |
| DNG | Lossless | Maximum | No | RAW archive (universal format) |
| HEIF/HEIC | Lossy | Excellent | No | Apple ecosystem, 50% smaller than JPEG |

---

## Export Settings by Use Case

### Social Media Platforms

| Platform | Dimensions | Format | Quality | Notes |
|----------|-----------|--------|---------|-------|
| Instagram Feed | 1080×1350px (4:5) | JPEG | 85% | Vertical preferred for feed |
| Instagram Story | 1080×1920px (9:16) | JPEG | 85% | Full-screen vertical |
| Facebook | 2048×2048px max | JPEG | 85% | Auto-compressed by platform |
| Twitter/X | 1600×900px (16:9) | JPEG/PNG | 85% | PNG for graphics |
| LinkedIn | 1200×627px | JPEG | 85% | Professional, banner format |
| Pinterest | 1000×1500px (2:3) | JPEG | 80% | Tall format performs best |
| Website/blog | 2048px long edge | JPEG/WebP | 80-85% | Optimize for load speed |

### Print Export

| Print Size | Minimum Resolution | File Format | Color Space |
|-----------|-------------------|-------------|-------------|
| 4×6" | 1200×1800px (300 DPI) | JPEG 100% or TIFF | sRGB for consumer labs |
| 8×10" | 2400×3000px (300 DPI) | JPEG 100% or TIFF | sRGB or Adobe RGB |
| 16×20" | 4800×6000px (300 DPI) | TIFF | Adobe RGB |
| 24×36" | 7200×10800px (300 DPI) | TIFF | Adobe RGB |
| Canvas/fine art | Max resolution | TIFF 16-bit | Adobe RGB or ProPhoto |

---

## Sharpening for Output

### Output Sharpening

| Output | Amount | Radius | Detail | Masking |
|--------|--------|--------|--------|---------|
| Screen (web) | 60-80 | 0.8-1.0 | 25-35 | 20-40 |
| Matte print | 80-100 | 1.0-1.2 | 30-40 | 10-30 |
| Glossy print | 60-80 | 0.8-1.0 | 25-35 | 20-40 |
| Large print (>16") | 40-60 | 0.5-0.8 | 20-30 | 30-50 |

### Lightroom Export Sharpening
- Choose output target: Screen, Matte Paper, Glossy Paper
- Amount: Low, Standard, High
- Standard works for most cases
- Use High for heavily downscaled images

---

## Color Management

### Color Space Selection

| Color Space | Gamut | Use Case |
|------------|-------|----------|
| sRGB | Standard | Web, social media, consumer print |
| Adobe RGB | Wide | Professional print, lab printing |
| ProPhoto RGB | Very wide | Editing workspace, archive |
| Display P3 | Wide | Apple devices, modern displays |

### Soft Proofing (Lightroom)
1. Enable Soft Proofing (S key in Develop)
2. Select target profile (printer ICC profile)
3. Choose rendering intent (Perceptual for photos)
4. Adjust image to compensate for gamut limitations
5. Create virtual copy for print-specific version

---

## Client Delivery

### Gallery Platforms

| Platform | Features | Pricing | Best For |
|----------|----------|---------|----------|
| Pixieset | Online gallery, download, print sales | Free-$300/yr | Wedding/portrait photographers |
| ShootProof | Gallery, contracts, invoicing | $120-360/yr | Full studio management |
| Pic-Time | Gallery, AI culling, print store | Free-$400/yr | Modern interface |
| Google Drive | Simple sharing | Free-$10/mo | Quick client delivery |
| Dropbox | File sharing, comments | Free-$20/mo | Large file delivery |

### Delivery Workflow
1. Final review of all selected images
2. Export with client-specific settings
3. Upload to delivery platform
4. Add password protection if needed
5. Send notification with download instructions
6. Follow up after 48 hours if not accessed
7. Archive: keep originals and finals for 1-2 years minimum

### File Naming Convention
```
[Date]_[Client]_[Sequence]_[Variant].jpg
Example: 20240315_Johnson_001_web.jpg
```
