# Vocal Recording Troubleshooting

Diagnosing and resolving common technical and performance issues during vocal recording sessions.

---

## Audio Quality Issues

### Noise and Interference

| Symptom | Likely Cause | Diagnosis | Fix |
|---------|-------------|-----------|-----|
| Constant hiss | High preamp gain, noisy preamp | Listen with mic disconnected — if hiss remains, it is the preamp | Use a higher output mic, lower gain, or upgrade preamp |
| 60/50 Hz hum | Ground loop, electromagnetic interference | Hum disappears when you disconnect the mic cable from the preamp | Use balanced cables, add a ground lift adapter, move away from power sources |
| Intermittent crackle | Bad cable, loose connection, digital clocking issue | Wiggle the cable while monitoring — crackle follows movement | Replace cable, check all connections |
| USB interference | Computer or USB hub noise coupling into the audio path | Noise appears only when recording via USB interface | Use a powered USB hub, try a different USB port, use a ferrite choke on the cable |
| HVAC rumble | Air conditioning or heating system vibration | Low-frequency rumble that disappears when HVAC is off | Turn off HVAC during recording, apply high-pass filter at 80 Hz |

### Distortion and Clipping

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Digital clipping (flat-topped waveform) | Input level too hot, peaks above 0 dBFS | Lower preamp gain until peaks reach -12 to -6 dBFS |
| Preamp distortion (fuzzy, not flat-topped) | Preamp overloaded before A/D conversion | Engage pad on mic or preamp (-10 or -20 dB), increase distance |
| Capsule overload | Extremely loud source overwhelming the mic | Use a dynamic mic instead of condenser, add external pad |
| DAW plugin distortion | Insert plugin adding gain | Check plugin input/output levels, reduce plugin input gain |

### Phase and Cancellation Issues

When using multiple microphones:
- **Symptom**: Thin, hollow sound when both mics are summed
- **Cause**: Mics at different distances from the source, causing phase cancellation
- **Fix**: Apply the 3:1 rule (second mic at least 3× the distance of the first mic from the source), or flip phase on one channel and listen for improvement

## Performance Issues

### Vocalist Cannot Hear Themselves

| Cause | Solution |
|-------|----------|
| Headphone mix too quiet | Increase vocalist channel in the headphone send |
| Latency too high (noticeable delay) | Lower audio buffer size to 128 samples, enable direct monitoring on interface |
| Wrong headphone output selected | Check DAW output routing and interface headphone source |
| Headphones not loud enough | Use higher impedance headphones with a dedicated headphone amp |

### Timing and Pitch Problems

| Issue | Diagnosis | Session Fix | Post-Production Fix |
|-------|-----------|-------------|-------------------|
| Rushing (ahead of beat) | Vocalist consistently early | Increase click volume, simplify headphone mix | Time-stretch or manual nudging |
| Dragging (behind beat) | Vocalist consistently late | Add a rhythmic element to headphone mix | Time-stretch or manual nudging |
| Pitch drift on sustained notes | Vocalist loses pitch center on long notes | Take breaks, warm up, try shorter phrases | Melodyne or Auto-Tune correction |
| Key confusion on harmonies | Vocalist cannot find the harmony note | Provide a guide harmony track in headphones | Re-record with guide, or pitch-correct |

### Vocal Fatigue

Signs of vocal fatigue:
- Voice becomes hoarse or breathy
- Pitch accuracy decreases
- High notes become strained
- Vocal tone thins out

**Prevention and response**:
1. Warm up before the session (5-10 minutes of gentle scales and humming)
2. Keep water available (room temperature, not cold)
3. Take 10-minute breaks every 45 minutes
4. Record demanding sections (high notes, belting) early in the session
5. If fatigue sets in, stop recording — pushing through produces unusable takes and risks vocal damage
6. Schedule intensive sessions with at least 24 hours between them

## Equipment Troubleshooting

### Microphone Not Detected

1. Check phantom power (+48V) is enabled on the preamp/interface (required for condenser mics)
2. Try a different XLR cable
3. Try the mic on a different preamp channel
4. Test with a different microphone to isolate whether the issue is the mic or the interface
5. On USB mics: check that the correct input device is selected in DAW and OS audio settings

### Latency Issues

| Scenario | Buffer Size | Expected Latency | Action |
|----------|------------|------------------|--------|
| Recording | 64-128 samples | 3-6 ms | Minimal, use this for tracking |
| Recording with plugins | 256 samples | 6-12 ms | Acceptable with monitoring through DAW |
| Mixing only | 512-1024 samples | 12-23 ms | Fine, no real-time monitoring needed |
| Latency still too high | Any | > 20 ms | Enable direct monitoring (bypasses DAW), or use a lower-latency driver (ASIO on Windows) |

### Session Recovery

If something goes wrong during a session:
- **DAW crash**: Most DAWs auto-save every few minutes; check the recovery folder
- **Accidental deletion**: Use undo (Ctrl/Cmd+Z) immediately; check the DAW's audio files folder for the raw recording
- **Power failure**: Audio files written to disk are usually recoverable; re-open the session and locate missing media
- **Corrupted session file**: Open the most recent backup; DAWs typically save `.bak` files alongside the main session file
