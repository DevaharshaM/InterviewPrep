# UART – Universal Asynchronous Receiver/Transmitter

UART is a widely used [serial communication](https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/Communication%20basics.md) protocol in embedded systems. It is simple, asynchronous, and ideal for point-to-point data transfer over short distances.

---

## Key Characteristics

- **Type**: Serial, Asynchronous
- **Lines Used**: TX (Transmit), RX (Receive), GND
- **Direction**: Full-duplex (transmit and receive simultaneously)
- **Clock**: Not shared; relies on internal timing

---

### UART Wiring Diagram

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/uart/block.png">
  <figcaption>Figure 1: UART Block Diagram</figcaption>
</figure>

---

## What is Baud Rate?

**Baud rate** is the number of **signal transitions (symbols)** transmitted per second over a communication channel.

- In UART, **one symbol typically equals one bit**, so the baud rate often equals the bit rate.
- For example, a baud rate of `9600` means **9600 bits per second** are transmitted.

### Key Points:
- **Symbol ≠ Bit** in general communication theory — but **in UART**, they are usually the same.
- **Both transmitter and receiver** must use the same baud rate to correctly interpret data.
- Common values: `9600`, `19200`, `38400`, `115200`, `1,000,000` (1M) bps.

### Why Baud Rate Matters:
- If the baud rate is mismatched between devices, **data corruption** occurs — the receiver will misread where bits start and stop.
- Higher baud rates allow **faster communication** but are more sensitive to noise and clock inaccuracies.

### Example:
At `9600` baud, one bit is transmitted every **104.17 microseconds**.

---

## Frame Format

A typical UART data frame:

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/uart/frame.png">
  <figcaption>Figure 2: UART Frame Format</figcaption>
</figure>

<br>A typical UART data frame includes:

- **Start Bit**: Signals the beginning of transmission (always LOW)
- **Data Bits**: Typically 8 bits
- **Parity Bit** (optional): For basic error checking
- **Stop Bit(s)**: Signals the end of transmission (always HIGH)

> Example format: **8N1** = 8 data bits, No parity, 1 stop bit

---

## Advantages

- Simple hardware and software implementation
- Fewer wires are needed
- Ideal for debugging and diagnostics (serial terminals)

---

## Limitations

- No built-in addressing (point-to-point only)
- Not suitable for multi-master or multi-slave systems
- Slower than synchronous protocols like SPI

---

## Common Applications

- Serial terminals (e.g., PuTTY, Tera Term)
- GPS receivers
- Bluetooth modules (e.g., HC-05)
- MCU serial prints

---

# Bonus: USART protocol

**USART** stands for **Universal Synchronous/Asynchronous Receiver/Transmitter**. It is a more versatile version of UART found in many microcontrollers (e.g., STM32, AVR).

### How is it different from UART?

| Feature         | UART                         | USART                            |
|------------------|-------------------------------|------------------------------------|
| Clock Line       | No (asynchronous only)        | Optional (can operate synchronously) |
| Communication    | Asynchronous only             | Asynchronous **and** synchronous  |
| Flexibility      | Fixed                         | More configurable                 |

### Synchronous Mode in USART:

In **synchronous mode**, USART can:
- Share a **common clock line** with another device
- Operate similarly to SPI (but slower and with different framing)
- Transmit data with higher timing accuracy

> Many applications still use USART in **asynchronous mode only**, effectively acting like UART.

---

# Bonus: Physical Layer Standards

UART by itself is just a **digital logic-level protocol** (typically 3.3V or 5V). To communicate over longer distances or to external devices, UART is often paired with **physical layer standards** like RS-232 or RS-485.

---

### RS-232

- Oldest and most widely known serial standard.
- Common in PCs (legacy COM ports), GPS modules, modems.

| Feature         | RS-232                      |
|------------------|-----------------------------|
| Signal Type     | Single-ended                |
| Voltage Levels  | ±3V to ±15V                 |
| Max Distance    | ~15 meters                  |
| Max Devices     | 1:1 communication only       |
| Cable           | DB9/DB25 connectors         |

> Requires a level shifter (e.g., **MAX232**) to connect RS-232 to a UART-capable MCU.

---

### RS-485

- Robust industrial standard, especially in noisy environments and long cable runs.
- Common in automation (Modbus RTU), HVAC, motor control.

| Feature         | RS-485                      |
|------------------|-----------------------------|
| Signal Type     | Differential (A/B lines)    |
| Voltage Levels  | Typically ±1.5V to ±5V      |
| Max Distance    | Up to 1200 meters           |
| Max Devices     | 32+ (multi-drop network)    |
| Mode            | Half-duplex or full-duplex  |

> RS-485 requires external transceivers (e.g., **MAX485**) and usually implements **half-duplex UART** communication.

---

### Summary Table

| Feature        | RS-232       | RS-485            |
|----------------|--------------|-------------------|
| Distance       | ~15 m        | ~1200 m           |
| Devices        | 2 (point-to-point) | 32+ (multi-drop) |
| Signaling      | Single-ended | Differential      |
| Noise Immunity | Low          | High              |
| Use Case       | Legacy PCs, GPS | Industrial, Modbus |

