# DAC – Digital to Analog Converter

A **Digital to Analog Converter (DAC)** performs the reverse operation of an ADC — it takes a digital value (binary number) and converts it into a corresponding analog voltage or signal.

---

## Why Do We Need DAC?

Embedded systems often need to **generate analog outputs**, such as:
- Audio waveforms
- Variable voltages for control
- Analog reference signals

DAC enables the microcontroller to **interface with the analog world** by synthesizing smooth, continuous waveforms from discrete digital data.

---

## 🔍 Basic Formula

For an **N-bit DAC** with reference voltage `Vref`:

Analog Output = (Digital Input / (2^N - 1)) × Vref

- `Digital Input`: Binary number sent to DAC (e.g., 0 to 255 for 8-bit)
- `Vref`: The maximum analog output voltage
- `N`: DAC resolution in bits

**Example**:  
8-bit DAC with `Vref = 3.3V`, digital input = 128  
Output = (128 / 255) × 3.3V ≈ 1.65V

---

## Key Parameters

| Term             | Meaning                                      |
|------------------|----------------------------------------------|
| **Resolution**   | Number of bits (e.g., 8-bit, 12-bit)         |
| **Settling Time**| Time to stabilize to final output voltage    |
| **Glitch Energy**| Spikes during code transitions               |
| **Linearity**    | How evenly the output steps scale            |

---

## Common DAC Architectures

| Type            | Principle                                    | Use Case                    |
|-----------------|----------------------------------------------|-----------------------------|
| **R-2R Ladder** | Uses resistors in a ladder network           | Most MCUs (basic output)    |
| **Weighted Resistor** | Uses different resistors per bit       | Older/simple implementations |
| **Delta-Sigma** | Converts digital input into high-rate stream | Audio-grade output          |
| **PWM + Filter**| Not a true DAC, but simulates one using PWM  | Low-cost analog output      |

> Note: **PWM-based DAC** is popular in MCUs without a true DAC (using a low-pass RC filter).

---

## How DAC Works

1. Digital value is written to a DAC register
2. Internal circuitry (e.g., resistor network or modulator) generates equivalent voltage
3. Analog voltage is output on DAC pin
4. Can be updated continuously to generate waveforms (sine, triangle, etc.)

---

## Applications

- Audio signal generation (e.g., MP3 playback)
- DC voltage control (for op-amp circuits or reference signals)
- Signal generation (sine, square, ramp)
- Motor control and dimming (via analog signals)
