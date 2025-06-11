# I²C – Inter-Integrated Circuit

I²C (pronounced “I-squared-C” or “I-two-C”) is a [**synchronous**](https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/Communication%20basics.md), **multi-master**, **two-wire** communication protocol developed by Philips. It is widely used for short-distance communication between microcontrollers and peripherals like sensors, RTCs, and EEPROMs.

---

## Key Characteristics

- **Type**: Serial, Synchronous
- **Lines Used**: SDA (Data), SCL (Clock)
- **Speed Modes**:
  - Standard: 100 kbps
  - Fast: 400 kbps
  - Fast Plus: 1 Mbps
  - High-Speed: 3.4 Mbps
- **Topology**: Typically single-master, multi-slave (spec supports multi-master with arbitration)
- **Pull-ups required** on both SDA and SCL

---

## How It Works

I²C uses a **shared bus** with two lines:
- **SDA**: Serial Data Line (bidirectional)
- **SCL**: Serial Clock Line (controlled by the master)

### I²C Wiring Diagram 

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/blockI2C.png">
  <figcaption>Figure 1: I2C Block Diagram</figcaption>
</figure>

> The master controls both data and clock lines, while multiple slaves listen and respond based on addressing.

---

## I²C Frame Format

A standard I²C data transfer consists of a **start condition**, followed by **address and data phases**, with **ACK/NACK bits** in between, and ends with a **stop condition**.

### I²C Frame Format

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/frameI2C.png">
  <figcaption>Figure 2: I2C Frame Format</figcaption>
</figure>

<br><br>Here’s a breakdown of each field:
| Field             | Size      | Description                                                                 |
|------------------|-----------|-----------------------------------------------------------------------------|
| **START**        | 1 bit     | Indicates beginning of communication (SDA goes LOW while SCL is HIGH)      |
| **Slave Address**| 7 or 10 bits | Unique ID of the target device on the bus                                  |
| **R/W Bit**      | 1 bit     | `0` = Write, `1` = Read                                                      |
| **ACK/NACK**     | 1 bit     | Receiver pulls SDA LOW to acknowledge (`ACK`) or keeps HIGH for NACK       |
| **Data Byte**    | 8 bits    | Actual payload byte sent/received                                           |
| **ACK/NACK**     | 1 bit     | Acknowledgment after each byte                                              |
| **STOP**         | 1 bit     | SDA goes HIGH while SCL is HIGH, ending the transaction                     |

---

## Start and Stop Conditions

The **start and stop conditions** are special states that signal the beginning and end of an I²C transaction.

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/conditionI2C.png">
  <figcaption>Figure 3: I2C START-STOP Conditions Timing Diagram</figcaption>
</figure>



- **Start condition**: SDA goes LOW while SCL is HIGH  
- **Stop condition**: SDA goes HIGH while SCL is HIGH

---

## Basic Data Transfer Flow

Once communication is initiated, the flow typically looks like this:

1. **Master sends START**
2. **Master sends 7-bit address + R/W bit**
3. **Slave acknowledges**
4. **Master or slave sends/receives data byte(s)**
5. **ACK/NACK exchanged after each byte**
6. **Master sends STOP**

> This process can repeat if multiple bytes are to be transferred in sequence.

---

## Clock Stretching

**Clock stretching** allows a slave to **hold the SCL line LOW** to delay the master from continuing.

### Why It's Needed:
- Some slaves (like EEPROMs or sensors) may need more time to prepare data.
- Master must monitor the clock line before sending the next bit.

> Clock stretching is optional — not all masters support it well.

---

## Arbitration in I²C (Multi-Master Capability)

While rarely used in practice, I²C supports **multi-master operation** with built-in arbitration:

- If two masters transmit at once, each watches SDA.
- If a master sends a HIGH (recessive) but sees a LOW (dominant), it **loses arbitration** and stops.
- The transaction continues non-destructively by the winning master.

> This makes I²C multi-master safe, though most systems still use **single-master** setups.

---

## Advantages of I²C

- Only **two wires** needed regardless of slave count
- Supports **multiple devices** via addressing
- Works well for **low-speed communication**
- **Standardized protocol** with wide MCU and peripheral support
- Built-in **ACK/NACK** and arbitration handling

## Limitations of I²C

- Limited speed compared to SPI
- **Bus capacitance** and pull-up resistors limit distance and device count
- Slower response due to shared bus
- Risk of **bus lock-up** if a slave holds SDA low
- Requires **careful timing and software handling** for robust systems

  ---

# Bonus: Advanced and Practical I²C Features

## Interrupt Pin for Event Notification

Many I²C peripherals provide a separate **INT pin** to notify the microcontroller when data is ready or a threshold is crossed.

- Allows the MCU to **wait in sleep mode** and react only on interrupt
- Common in sensors (e.g., accelerometers, proximity sensors)
- Reduces I²C bus traffic and improves power efficiency

> This pin is **not part of the I²C protocol**, but enhances performance in interrupt-driven designs.

## SMBus Compatibility

**SMBus** is a variant of I²C used in laptops, batteries, and power systems (e.g., fuel gauges, smart chargers).

- Stricter electrical & timing specs
- Defines standard commands (e.g., block read/write)
- Often used in conjunction with **PMBus** for power control

> Most I²C controllers can communicate with SMBus devices with minimal changes.

## 10-bit Addressing Support

While most I²C devices use **7-bit addresses**, the protocol also supports **10-bit addressing** for larger device ecosystems.

- First byte includes special `11110xx` prefix
- Rarely used — not all masters support it

> These extended features make I²C flexible for low-power, multi-sensor, and power-aware systems — not just simple data transfer.
