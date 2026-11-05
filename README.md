# Effem

**Effem** is a 16-voice polyphonic synthesizer written in [Faust](https://faust.grame.fr/). It features a versatile dual-oscillator FM/AM architecture, a dedicated pitch-envelope "bubble" oscillator, a noise channel, and a lush, custom feedback reverb algorithm (`Viverb`). 

---

## ✨ Features

- **16-Voice Polyphony**: Full MIDI support with smooth voice stealing.
- **Dual Oscillator Core**: Carrier and Modulator oscillators with a dedicated FM/AM routing switch.
- **"Bubble" Pitch Envelope (Osc 3)**: A secondary oscillator with selectable waveforms (Sine, Triangle, Square, Sawtooth) and a dedicated pitch envelope (Attack, Decay, Sustain) for dynamic, percussive, or sweeping frequency modulation.
- **Noise Generator**: Adjustable white noise channel for adding texture, percussion, or wind-like elements.
- **Dynamic Effects Chain**: 
  - Waveshaping overdrive with gain compensation.
  - Resonant low-pass filter with dedicated LFO modulation.
  - **Viverb**: A custom, high-quality feedback reverb algorithm featuring nested all-pass diffusers, modulated delay lines, and comprehensive damping/size controls.
- **Standard ADSR Envelope**: Full control over amplitude shaping.

---

## 🌊 Signal Flow

```text
[Osc 1 (Carrier)] ──┐
[Osc 2 (Modulator)]─┤──> (FM/AM Mix) ──┐
[Osc 3 (Bubble)] ───┤                  │
[Noise Channel] ────┘                  │
                                       ▼
                              [Amplitude ADSR Envelope]
                                       │
                                       ▼
                              [Waveshaping Drive]
                                       │
                                       ▼
                           [Resonant Low-Pass Filter + LFO]
                                       │
                                       ▼
                         [Viverb Reverb (Dry/Wet Mix)]
                                       │
                                       ▼
                               [Master Output]
```

---

## 🎚️ Controls Reference

The synthesizer UI is logically grouped into the following sections:

### Oscillator 1 (Carrier)
| Control | Description |
| :--- | :--- |
| **PI slide** | Multiplier for the carrier phase/frequency (creates unique harmonic shifts). |
| **Osc1 Level** | Output volume of the carrier oscillator. |
| **FM/AM Switch** | Toggles between Frequency Modulation (FM) and Amplitude Modulation (AM) routing from Osc 2. |

### Modulator (Osc 2)
| Control | Description |
| :--- | :--- |
| **Modulator Frequency** | Base frequency of the modulating oscillator. |
| **Modulation Index** | Depth of the modulation applied to the carrier. |
| **Modulator Level** | Output volume of the modulator (useful for AM or audible FM). |

### Oscillator 3 (Bubble / Pitch Envelope)
| Control | Description |
| :--- | :--- |
| **Waveform Selector** | Choose between Sine, Triangle, Square, or Sawtooth. |
| **Freq** | Base frequency of the pitch envelope oscillator. |
| **Pitch Envelope** | Attack, Decay, and Sustain controls for the pitch sweep. |
| **LFO Freq / Depth** | Modulates the base frequency of Osc 3 for added movement. |
| **Enable FM** | Routes Osc 3 to modulate the main oscillators (or keeps it independent). |
| **Mute** | Silences Osc 3 output. |

### Envelope & Filter
| Control | Description |
| :--- | :--- |
| **ADSR** | Standard Attack, Decay, Sustain, and Release for amplitude. |
| **Gain** | Pre-filter amplitude scaling. |
| **Cutoff Frequency** | Resonant low-pass filter cutoff point. |
| **Q** | Filter resonance. |
| **Filter LFO** | Frequency and Depth controls to modulate the filter cutoff. |

### Mix & Effects
| Control | Description |
| :--- | :--- |
| **Noise** | Level of the white noise channel. |
| **Drive** | Waveshaping distortion amount. |
| **Drive Compensate** | Post-drive volume adjustment to prevent clipping. |
| **Master** | Global output volume. |
| **Viverb** | Custom reverb with controls for Delay Time, Damping, Size, Diffusion, Feedback, Modulation Depth, Modulation Frequency, and Dry/Wet mix. |

---

## 🚀 Installation & Usage

Effem is a standard Faust DSP file (`.dsp`). You can compile it into various plugin formats or standalone applications depending on your needs.

### Prerequisites
- [Faust Compiler](https://faust.grame.fr/) installed on your system.

### Compilation Examples

**1. Standalone JACK Application (Linux/macOS)**
```bash
faust2jaudi effem.dsp
```

**2. LV2 Plugin (for use in DAWs like Ardour, Carla, Bitwig)**
```bash
faust2lv2 effem.dsp -o effem.lv2
```

**3. VST3 Plugin (requires Faust VST3 architecture)**
```bash
faust2vst3 effem.dsp -o effem.vst3
```

**4. Web Audio (for browser-based testing)**
```bash
faust2webaudio effem.dsp -o effem.html
```

*Note: For DAW integration, load the compiled plugin and ensure your host supports polyphonic MIDI input.*

---


This project is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
