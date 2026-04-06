# MIDI Production Troubleshooting

Common problems and solutions for MIDI latency, routing, timing, virtual instrument, and controller issues.

---

## Latency Issues

### Input Latency (Delay Between Playing and Hearing)

| Cause | Diagnosis | Solution |
|-------|-----------|----------|
| High audio buffer size | Check DAW audio settings (buffer > 512 samples) | Lower buffer to 128-256 samples during recording |
| CPU overload | DAW CPU meter spiking, audio crackling | Freeze/bounce heavy tracks, increase buffer, disable plugins on inactive tracks |
| USB hub bottleneck | Latency only with hub-connected controllers | Connect MIDI controller directly to computer USB port |
| Driver issues (Windows) | Latency even with low buffer | Install ASIO driver (ASIO4ALL for budget interfaces, manufacturer ASIO for pro interfaces) |
| Bluetooth MIDI | Inherent 10-30ms latency | Use USB or DIN MIDI for performance; reserve Bluetooth for non-time-critical input |

### Round-Trip Latency Measurement

1. Set buffer to your target size (e.g., 128 samples)
2. Calculate theoretical latency: `(Buffer Size / Sample Rate) × 2 = round-trip`
3. At 128 samples / 44.1 kHz: ~5.8ms round-trip (perceptible but playable)
4. At 256 samples / 44.1 kHz: ~11.6ms (acceptable for keys, borderline for drums)
5. At 512 samples / 44.1 kHz: ~23.2ms (mixing only, not playable)

## Routing Problems

### No Sound from Virtual Instrument

Troubleshooting checklist:
1. **MIDI input**: Is the track's MIDI input set to the correct controller or "All MIDI Inputs"?
2. **MIDI channel**: Does the controller channel (usually Ch 1) match the instrument's receive channel?
3. **Monitor/Record enable**: Is the track armed or monitor-enabled?
4. **Audio output**: Is the instrument track routed to the master bus or an active output?
5. **Instrument loaded**: Is a patch/preset actually loaded in the virtual instrument?
6. **MIDI activity indicator**: Does the DAW show MIDI input activity when you play? If not, the issue is upstream of the DAW.

### MIDI Not Reaching the DAW

1. Check OS MIDI settings (macOS: Audio MIDI Setup; Windows: Device Manager > Sound)
2. Verify the controller appears as a MIDI device
3. Try a different USB cable or port
4. On macOS, reset the MIDI configuration: delete the MIDI device in Audio MIDI Setup and reconnect
5. On Windows, reinstall the controller's driver

### Multi-Timbral Routing

When using a multi-timbral instrument (e.g., Kontakt with multiple instruments):
- Assign each instrument to a separate MIDI channel (Ch 1-16)
- Create separate MIDI tracks in the DAW, each targeting a different channel
- Route each instrument's audio output to a separate DAW mixer channel for independent mixing

## Timing and Quantization Issues

### MIDI Clock Drift

| Symptom | Cause | Fix |
|---------|-------|-----|
| Instruments gradually go out of sync | Multiple MIDI clock sources | Designate one master clock (usually the DAW) |
| Timing is sloppy after long sessions | Clock jitter in USB MIDI | Use a dedicated hardware MIDI interface with tight clock |
| External synth is ahead/behind | MIDI clock transmission delay | Use the DAW's MIDI clock offset/delay compensation setting |

### Quantization Artifacts

- **Too strict**: 100% quantize to grid removes human feel. Use 50-75% strength instead.
- **Wrong grid**: Quantizing swing patterns to straight 16ths destroys the groove. Match the quantize grid to the intended rhythm.
- **Note overlaps**: After quantization, check for overlapping notes that cause stuck notes or re-triggers.
- **Preserve velocity**: Ensure quantization affects only timing, not velocity or note length (unless intended).

## Virtual Instrument Issues

### CPU Spikes and Audio Dropouts

1. **Freeze tracks**: Render MIDI to audio for tracks you are not actively editing
2. **Increase buffer**: Raise to 512-1024 for mixing (not tracking)
3. **Reduce polyphony**: Lower the max voices in the instrument settings
4. **Use sample purge**: In Kontakt and similar samplers, purge unused samples from RAM
5. **SSD storage**: Ensure sample libraries are on SSD, not spinning disk

### Stuck Notes (Note Hanging After Release)

- Send an "All Notes Off" MIDI message (CC 123, value 0 on all channels)
- Most DAWs have a panic button or key command for this
- If frequent: check for duplicate MIDI routings sending note-on without note-off
- Check for MIDI feedback loops (instrument output routed back to its input)

### Missing Articulations or Keyswitches

- Verify the keyswitch note range for the instrument (often C-2 to B-1 or C0 to B0)
- Ensure keyswitches are on the correct MIDI channel
- Check that the note velocity is above the instrument's minimum threshold
- Some instruments use CC switches instead of keyswitches — consult the instrument manual
