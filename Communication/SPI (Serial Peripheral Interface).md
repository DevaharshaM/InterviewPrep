# SPI – Serial Peripheral Interface

**SPI (Serial Peripheral Interface)** is a high-speed, [full-duplex](https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/Communication%20basics.md), synchronous serial communication protocol. It is commonly used for short-distance, high-throughput communication between microcontrollers and peripherals such as displays, ADCs, flash memory, and sensors.

---

## Key Characteristics

- **Type**: Serial, Synchronous
- **Mode**: Full-Duplex (data transmitted and received simultaneously)
- **Lines Used**:
  - **MOSI** – Master Out Slave In
  - **MISO** – Master In Slave Out
  - **SCLK** – Serial Clock 
  - **CS/SS** – Chip Select / Slave Select (individual line per slave)
- **Topology**: Single-master, multi-slave (using separate CS lines)
- **Clock Speed**: Ranges from hundreds of kHz to tens of MHz

---

## Basic Data Transfer Flow

1. Master pulls the **CS** line LOW to select the target slave.
2. Master toggles the **SCLK** to begin the transfer.
3. Data is shifted out via **MOSI** and received via **MISO** simultaneously.
4. After the desired number of bits, the **CS** line is pulled HIGH to complete the transaction.

---

## SPI Wiring Diagram

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/blockSPI.png">
 <figcaption>Figure 1: SPI Block Diagram</figcaption>
</figure>

---

## CPOL and CPHA – Clock Polarity and Phase

SPI supports **four modes** defined by **CPOL** (Clock Polarity) and **CPHA** (Clock Phase). These determine how data is sampled and shifted relative to the clock signal.

| Mode | CPOL | CPHA | Clock Idle | Data Captured On     | Description |
|------|------|------|------------|-----------------------|-------------|
| 0    | 0    | 0    | LOW        | Rising edge (1st)     | Default on many devices |
| 1    | 0    | 1    | LOW        | Falling edge (2nd)    | Data valid on second edge |
| 2    | 1    | 0    | HIGH       | Falling edge (1st)    | Idle clock high, sample on first edge |
| 3    | 1    | 1    | HIGH       | Rising edge (2nd)     | Both clock idle and sampling on HIGH transitions |

> **Master and slave must be configured to use the same mode** for communication to work correctly.

---

## SPI Frame Format 

SPI has **no standardized frame format** like I²C or CAN. Instead, each device defines its own data protocol. However, a typical transaction might look like:

| Segment        | Description                             |
|----------------|------------------------------------------|
| **Command**    | Tells the slave what operation to perform |
| **Address**    | Location in memory or register map       |
| **Data Byte(s)**| Data to write, or empty space to read into |

The **CS line** is often used to indicate the boundary of a data frame. Some devices expect CS to stay LOW throughout a multi-byte transaction; others may latch on each byte.

---

## Advantages of SPI

- **High Speed**: SPI can operate at much higher speeds than UART or I²C, typically tens of Mbps.
- **Full-Duplex Communication**: Data can be sent and received simultaneously, improving throughput.
- **Simple Hardware Interface**: Just four lines needed, no complex logic for addressing or arbitration.
- **No Fixed Data Frame**: Flexible for communicating with a wide variety of devices.
- **Multiple Slaves**: Supports multi-slave configurations using separate CS lines.
- **Deterministic Timing**: Data is shifted based on clock edges — good for time-sensitive applications.
  
## Limitations of SPI

- **No built-in addressing** — master must manage each slave using a separate CS line
- **No built-in error checking** — must be handled in software
- Not ideal for **multi-master systems**
- Not suitable for **long-distance communication** due to lack of differential signaling

---

# Bonus: Advanced and Practical I²C Features

## Daisy-Chaining SPI Devices

Some SPI peripherals (like shift registers or daisy-chainable LEDs) support chaining:

- The **MISO** of one slave connects to the **MOSI** of the next
- Data is clocked **through all devices** in one large stream
- Requires special command/data formatting

> Useful when you want to reduce the number of CS lines — but you must manage bit placement carefully.
