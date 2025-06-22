# Ethernet in Embedded Systems

**Ethernet** is a widely used wired communication protocol defined under the IEEE 802.3 standard. It provides reliable and fast data transmission over a local area network (LAN), making it ideal for industrial and embedded applications requiring deterministic or high-throughput communication.

---

## What is Ethernet?

Ethernet is a **packet-based communication** system where devices (nodes) exchange data using MAC (Media Access Control) addresses over a physical medium like twisted pair cables or fiber optics.

---

## Ethernet Frame Structure

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Networking%20%26%20Connectivity/Ethernet.png">
  <figcaption>Figure 1: Ethernet Frame Format</figcaption>
</figure>

<br>Each field can be described as -<br>
| Field                  | Size (Bytes)   | Description                                                  |
|-----------------------|----------------|--------------------------------------------------------------|
| Preamble              | 7              | Synchronization pattern (101010...)                          |
| Start Frame Delimiter | 1              | Marks beginning of the frame                                 |
| Destination Address   | 6              | Receiver’s MAC address                                       |
| Source Address        | 6              | Sender’s MAC address                                         |
| Length / Type         | 2              | Payload size or protocol type (e.g., 0x0800 for IPv4)        |
| Payload (Data)        | 46–1500        | Actual data being transmitted                                |
| CRC                   | 4              | Error checking via Cyclic Redundancy Check                   |

> Minimum frame size: 64 bytes, Maximum (standard): 1518 bytes (not including preamble)

---

## MAC vs IP Address

- **MAC Address**: Hardware address; unique to each Ethernet device (Layer 2)
- **IP Address**: Logical address assigned by network or user (Layer 3)

---

## How Ethernet Works

1. **Each device** has a unique MAC address.
2. Frames are sent to the destination MAC.
3. **Switches** forward the frame to the correct port based on MAC.
4. CRC checks ensure data integrity.

---

## Collision Domains & Switches

- Older hubs used **CSMA/CD** (Carrier Sense Multiple Access / Collision Detection) to handle traffic.
- Modern switches eliminate collision domains by separating traffic per port.

---

## Ethernet in Embedded Systems

| Use Case                    | Example                              |
|-----------------------------|--------------------------------------|
| Industrial Ethernet         | PLCs, SCADA systems                  |
| Remote firmware updates     | Over-the-air updates via LAN         |
| Data logging and streaming  | Sensor networks with web access      |
| Communication gateway       | MCU + Ethernet for TCP/IP access     |

---

## Popular ICs and Solutions

- **LAN8720**, **ENC28J60**, **W5500**: Common Ethernet PHY chips
- Interfaces via **SPI**, **MII**, or **RMII**
- Supported in STM32, ESP32, NXP, etc.
