# Audio Restoration Fundamentals

Core concepts and techniques for repairing and cleaning audio recordings, covering noise types, analysis methods, and foundational restoration processes.

---

## Types of Audio Degradation

Understanding the type of degradation guides tool and technique selection:

| Degradation Type | Characteristics | Common Sources | Primary Tool |
|-----------------|-----------------|----------------|-------------|
| Broadband Noise | Constant hiss across frequency spectrum | Tape hiss, preamp noise, HVAC | Spectral denoising |
| Impulse Noise | Short, sharp transient spikes | Clicks, pops, crackle from vinyl | Declicker / Decrackler |
| Hum | Tonal, harmonic at 50/60 Hz | Ground loops, electromagnetic interference | Notch filter / Dehum |
| Clipping | Flat-topped waveform peaks | Overloaded input, digital overs | Declipping algorithm |
| Reverb/Room Tone | Excessive ambient reflection | Poor recording environment | Dereverb (limited) |
| Frequency Loss | Missing high or low end | Bandwidth-limited recording, degraded tape | EQ restoration, harmonic exciter |

## Signal Analysis Techniques

### Spectral Analysis

Use a spectrogram (time × frequency × amplitude) to visually identify noise patterns:
- **Constant horizontal lines**: Hum and harmonics (50/60 Hz + overtones)
- **Uniform color band across time**: Broadband noise floor
- **Vertical spikes**: Impulse noise (clicks, pops)
- **Bright blobs**: Transient events or artifacts

Configure the FFT size based on the analysis goal:
- **Short FFT (512-1024)**: Better time resolution for transient detection
- **Long FFT (4096-8192)**: Better frequency resolution for tonal noise identification

### Noise Profile Capture

Most spectral denoisers require a noise profile — a short sample (0.5-2 seconds) of noise-only audio. Select a section where no desired signal is present (pause between words, room tone before a take). The denoiser learns the noise spectrum and subtracts it from the full recording.

Guidelines for noise profile selection:
- Choose the longest clean noise section available
- Avoid sections with faint desired signal bleeding through
- If noise varies over time, capture multiple profiles and apply them to corresponding sections

## Foundational Restoration Workflow

Process audio degradation in this order to avoid artifacts:

1. **Declip** — Reconstruct clipped peaks before any other processing, since clipping distorts the waveform that all subsequent tools analyze
2. **Declick / Decrackle** — Remove impulse noise next, as clicks can confuse noise profiling
3. **Dehum** — Remove tonal hum (notch filters at fundamental and harmonics)
4. **Denoise** — Apply broadband noise reduction using the captured noise profile
5. **EQ correction** — Restore frequency balance lost to degradation or the recording medium
6. **Level normalization** — Adjust final gain to target loudness (e.g., -16 LUFS for podcasts, -14 LUFS for streaming)

### Key Principles

- **Less is more**: Over-processing introduces artifacts (warbling, metallic sound). Apply the minimum reduction needed.
- **A/B constantly**: Toggle the processor on/off and listen for artifacts in the desired signal.
- **Work in high resolution**: Process at the highest available bit depth and sample rate. Dither only on final export.
- **Preserve dynamics**: Avoid aggressive limiting or compression during restoration — address dynamics separately in mixing.

## Common Software Tools

| Tool | Strengths | Platform |
|------|-----------|----------|
| iZotope RX | Industry standard, comprehensive suite | Mac, Windows |
| Acon Digital Restoration Suite | Clean algorithms, good value | Mac, Windows |
| Audacity (free) | Basic noise reduction, click removal | Cross-platform |
| Adobe Audition | Spectral editing, noise print denoising | Mac, Windows |
| Steinberg SpectraLayers | Advanced spectral editing and separation | Mac, Windows |
