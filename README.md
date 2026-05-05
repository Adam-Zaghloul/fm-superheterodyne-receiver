# Auto-Scan FM Superheterodyne Radio Receiver

> FM band 88–108 MHz · TDA7088T superheterodyne IC · Varactor tuning · AFC · LM386 audio amp  
> **La Cité collégiale — RF & Telecommunications · Fall 2025**

---

## Photos

| PCB Top View | Assembled & Running |
|---|---|
| ![FM Radio PCB](../images/fm-radio.jpg) | ![FM Radio Running](../images/fm-radio-2.jpg) |

---

## Overview

Assembly, alignment, and troubleshooting of an **Elenco FM-88K auto-scan FM radio kit** — a real superheterodyne receiver covering the full commercial FM band (88–108 MHz). The project applied hands-on RF signal chain theory: antenna coupling, mixing, IF filtering, FM demodulation, automatic frequency control (AFC), and audio power amplification.

The receiver was aligned by adjusting coil L2 to set the correct scan start frequency (~88 MHz) and validated by successfully receiving multiple stations with no scan-lock failures.

---

## Specifications

| Parameter | Value |
|-----------|-------|
| Frequency range | 88 – 108 MHz |
| IF frequency | 10.7 MHz |
| Tuning method | Varactor diode (BB909/BB910) |
| Scan control | Auto-scan (S button) + Reset (R button) |
| Audio output | 8 Ω speaker via LM386 |
| Power supply | 9 V battery |
| Receiver IC | TDA7088T (or SC1088, SA1088, YD9088) |
| Audio amp IC | LM386 (gain 20–200) |

---

## Signal Chain

```
[Telescopic Antenna]
        │
[RF Input Circuit: L1, C5, C6, C7 — parallel resonant]
        │
[Mixer inside TDA7088T]
        │
[Local Oscillator (VCO) — frequency controlled by varactor D1 (BB910)]
        │
[IF Amplifier — fixed at 10.7 MHz]
        │
[FM Demodulator]
        │
[AFC — corrects VCO drift, maintains 10.7 MHz centre]
        │
[Audio Pre-Amp (mute control inside TDA7088T)]
        │
[LM386 Audio Power Amplifier (U2) — gain up to 200 with C21]
        │
[8 Ω Speaker]
```

---

## How Auto-Scan Works

1. **SCAN (S) button pressed** → positive voltage applied to TDA7088T pin 16 (Tuning Search input)
2. **C14 charges** → voltage on pin 16 rises continuously
3. **D1 (BB910 varactor)** — rising voltage reduces capacitance → local oscillator frequency increases
4. **Oscillator sweeps upward** until `Fo − Fs = 70 kHz` (station lock condition)
5. **Mute Control circuit detects lock** → halts C14 charging → AFC holds frequency stable
6. **RESET (R) button pressed** → C14 discharges → receiver returns to 88 MHz (band start)

---

## Key Components

| Ref | Component | Function |
|-----|-----------|----------|
| U1 | TDA7088T (SMD, pre-installed) | Complete FM superheterodyne front-end + AFC + FLL |
| U2 | LM386 | Low-voltage audio power amplifier |
| D1 | BB909 / BB910 varactor | Electronic tuning — capacitance varies with DC bias |
| D2 | 1N4001 | Rectifier / protection |
| D3 | Red LED | Power-on indicator |
| L1 | 6-turn coil | RF input resonant circuit |
| L2 | 4-turn coil | Oscillator tuning — adjusted for 88 MHz scan start |
| R6/S3 | 50 kΩ pot + switch | Volume control + power on/off |
| C14 | 0.1 µF | Tuning search charge capacitor |
| S1 (yellow) | Push-button | SCAN |
| S2 (red) | Push-button | RESET |

---

## Alignment Procedure

After assembly, the scan start frequency must be set to ~88 MHz:

1. Power on, press RESET, then SCAN
2. If first station received is **above 90 MHz** → press coils of L2 closer together (increases inductance)
3. If first station received is **below 87 MHz** → spread L2 coils apart (decreases inductance)
4. Iterate until scan reliably starts at the low end of the FM band

---

## Troubleshooting Performed

| Symptom | Cause | Fix |
|---------|-------|-----|
| No audio after assembly | Incorrect polarity on electrolytic caps | Verified and corrected C2, C18, C20 orientation |
| Scan would not lock | L2 coil spacing incorrect | Adjusted L2 for correct scan start frequency |
| Clicking but no station audio | U2 (LM386) functional, U1 suspect | Re-verified U1 pin voltages against reference chart |

---

## RF Concepts Applied

- **Superheterodyne architecture** — frequency conversion to a fixed IF (10.7 MHz) for consistent selectivity
- **Image frequency rejection** — RF stage suppresses signal at `Fo + 10.7 MHz`
- **Varactor tuning** — voltage-controlled capacitance replaces mechanical tuning gang
- **AFC (Automatic Frequency Control)** — DC correction voltage fed back to VCO, maintains lock against temperature drift
- **Class AB audio output** — LM386 biased for minimal crossover distortion with reasonable efficiency

---

## Skills Demonstrated

`RF signal chain` `Superheterodyne receiver` `Varactor tuning` `IF filtering` `FM demodulation` `AFC` `LM386 audio amplifier` `THT soldering` `RF alignment` `Oscilloscope` `Fault isolation` `IPC-A-610`

---

*Adam Zaghloul · La Cité collégiale · Fall 2025 · [adamzaghloul07@gmail.com](mailto:adamzaghloul07@gmail.com)*
