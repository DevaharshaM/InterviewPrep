# ADC – Analog to Digital Converter

An **Analog to Digital Converter (ADC)** is used to convert real-world analog signals (like voltage or current) into digital values that can be processed by a microcontroller.

---

## Why Do We Need ADC?

Microcontrollers operate on digital logic. However, most real-world inputs (temperature, sound, light, etc.) are analog in nature. The ADC enables a digital system to **understand and react to analog events**.

---

## Basic Formula

For an **N-bit ADC** and a reference voltage `Vref`:

Digital Output = (Vin / Vref) × (2^N - 1)

- `Vin`: Input analog voltage  
- `Vref`: Reference voltage (maximum measurable voltage)  
- `N`: Resolution of the ADC (e.g., 10-bit, 12-bit)

**Example**:  
With a 10-bit ADC, `Vref = 3.3V`, and `Vin = 1.65V`:  
Output = (1.65 / 3.3) × 1023 = 512

---

## How Does ADC Work?

1. **Sample**: The analog signal is captured (sampled) at a specific time.  
2. **Hold**: The signal is held steady using a Sample and Hold (S/H) circuit.  
3. **Quantize**: The voltage range is divided into discrete digital levels.  
4. **Encode**: The closest level is encoded into a binary number.

This process is typically controlled by:
- A **Start Conversion** trigger (software or timer)
- A selected **input channel** (ADC pin)
- A **reference voltage** (internal or external)
- An **ADC clock** for conversion timing

---

## Resolution and Step Size

| Bits | Levels | Step Size (for 3.3V) |
|------|--------|----------------------|
| 8    | 256    | ~12.9 mV             |
| 10   | 1024   | ~3.22 mV             |
| 12   | 4096   | ~0.81 mV             |
| 16   | 65536  | ~0.05 mV             |

> Higher resolution gives finer voltage measurement, but requires more time and memory.

---

## Types of ADCs

| Type                       | Principle                            | Use Cases                     |
|----------------------------|--------------------------------------|-------------------------------|
| **SAR (Successive Approximation)** | Binary search comparison | Most MCUs (e.g., STM32, AVR)  |
| **Delta-Sigma**            | Oversampling and noise shaping       | Audio, sensors (slow + precise) |
| **Flash**                  | Parallel comparators (very fast)     | Oscilloscopes, RF sampling    |
| **Dual-Slope**             | Integration over time                | Digital multimeters           |

---

## Applications

- Sensor interfacing (temperature, pressure, light)
- Battery voltage monitoring
- Audio input for DSP
- Touchscreens and capacitive sensing
