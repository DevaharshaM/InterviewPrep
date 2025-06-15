# DMA – Direct Memory Access

**Direct Memory Access (DMA)** is a hardware feature that allows data to be transferred **between memory and peripherals (or between memory locations)** without CPU intervention.

---

## Why Do We Need DMA?

Normally, the CPU handles every data transfer — for example, reading from ADC and storing the result in memory. But doing this repeatedly wastes CPU time.

With DMA:
- Data transfers happen **in the background**
- CPU is **free to perform other tasks**
- Improves efficiency and responsiveness

---

## How DMA Works

1. **DMA controller** is configured with:
   - Source address (e.g., ADC register)
   - Destination address (e.g., RAM)
   - Transfer size (in bytes/words)
   - Transfer mode (normal, circular, etc.)

2. Once triggered (manually or by peripheral event):
   - DMA takes control of the bus
   - Transfers the data block autonomously
   - Generates an interrupt on completion (optional)

---

## Transfer Modes

| Mode      | Description                                     |
|-----------|-------------------------------------------------|
| **Normal**   | Transfers a block once, then stops              |
| **Circular** | Automatically restarts after finishing — useful for continuous data (e.g., ADC sampling) |
| **Burst**    | Transfers multiple data items at once (efficient for memory-to-memory) |

---

## Common Use Cases

- **ADC to memory** (e.g., storing sampled sensor data)
- **Memory to DAC** (e.g., audio output waveform)
- **USART/SPI to memory** (e.g., buffered communication)
- **Memory-to-memory copy** (e.g., bulk data movement)

> DMA is particularly helpful when paired with **interrupts** or **timers** to automate sampling and response.

---

## Benefits of DMA

| Benefit              | Explanation                                   |
|----------------------|-----------------------------------------------|
| **Frees CPU**        | Reduces CPU load during repetitive transfers  |
| **Faster throughput**| Uses direct bus access — no instruction cycles |
| **Real-time capable**| Consistent timing for I/O, audio, ADC, etc.   |

---

## Example: ADC Sampling with DMA

- Timer triggers ADC at regular intervals
- ADC completes conversion
- DMA automatically transfers result to buffer
- CPU reads the buffer when needed

This removes the need for the CPU to poll ADC or handle every sample interrupt.
