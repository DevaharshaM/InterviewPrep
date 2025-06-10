# CAN – Controller Area Network

The Controller Area Network (CAN) is a robust, multi-master [serial communication](https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/Communication%20basics.md) protocol designed for real-time control applications. Originally developed by Bosch, it's widely used in automotive, industrial, and medical systems.

---

## Key Features

- **Type**: Serial, Multi-master, Message-based
- **Speed**: Up to 1 Mbps (CAN 2.0); higher for CAN FD
- **Reliability**: Error detection, fault confinement, priority-based arbitration
- **Standard**: Defined by **ISO 11898**

---

### CAN Wiring Diagram

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/blockCAN.png">
  <figcaption>Figure 1: CAN Block Diagram</figcaption>
</figure>

---

## CAN Frame Formats

CAN has two primary frame types defined under CAN 2.0:

- Standard Frame (2.0A)

- Extended Frame (2.0B)

### ➤ CAN 2.0A (Standard Frame)

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/frameCAN2.0A.png">
  <figcaption>Figure 2: CAN 2.0A Frame Format</figcaption>
</figure>

<br><br>Here’s a breakdown of each field:

| Field                          | Bits        | Description                                                            |
|--------------------------------|-------------|------------------------------------------------------------------------|
| SOF (Start of Frame)           |   1 bit     | Dominant bit ('0') to signal the start of transmission                 |
| Identifier                     | 11 bits     | Message priority & content identifier                                  |
| RTR                            |   1 bit     | Remote Transmission Request ('0' for Data Frame, '1' for Remote Frame) |
| IDE                            |   1 bit     | Identifier Extension ('0' indicates standard frame )                   |
| r0                             |   1 bit     | Received bit (Always '1' )                                             |
| DLC (Data Length Code)         |   4 bit     | Number of data bytes (0–8 )                                            |
| Data                           | 0-8 bytes   | Actual data payload (0 to 8 bytes)                                     |
| CRC (Cyclic Redundancy Check)  | 15 + 1 bits | CRC for error detection and a delimiter bit                            |
| ACK (Acknowledgement)          | 1 + 1 bits  | One bit for ACK from receivers + delimiter                             |
| EOF (End of Frame)             | 7 bits      | Recessive bits ('1') to signify end of transmission                    |
| IFS (Interframe Space)         | 3 bits      | Recessive bits ('1') separating frames on the bus                      |

### ➤ CAN 2.0B (Extended Frame)

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Communication/frameCAN2.0B.png">
  <figcaption>Figure 3: CAN 2.0B Frame Format</figcaption>
</figure>

<br><br>Here’s a breakdown of each field:

| Field                          | Bits        | Description                                                            |
|--------------------------------|-------------|------------------------------------------------------------------------|
| SOF (Start of Frame)           |   1 bit     | Dominant bit ('0') to signal the start of transmission                 |
| Identifier                     | 11 bits     | First part of the 29-bit identifier                                    |
| SRR                            |   1 bit     | Substitute Remote Request (Always Recessive '1')                       |
| IDE                            |   1 bit     | Identifier Extension ('1' indicates extended frame )                   |
| Identifier                     | 18 bits     | Remaining bits of the 29-bit ID                                        |
| RTR                            |   1 bit     | Remote Transmission Request ('0' for Data Frame, '1' for Remote Frame) |
| r1                             |   1 bit     | Received bit (Always '1' )                                             |
| r0                             |   1 bit     | Received bit (Always '1' )                                             |
| DLC (Data Lenth Code)          |   4 bit     | Number of data bytes (0–8 )                                            |
| Data                           | 0-8 bytes   | Actual data payload (0 to 8 bytes)                                     |
| CRC(Cyclic Redundancy Check)   | 15 + 1 bits | CRC for error detection and a delimiter bit                            |
| ACK (Acknowledgement)          | 1 + 1 bits  | One bit for ACK from receivers + delimiter                             |
| EOF (End of Frame)             | 7 bits      | Recessive bits ('1') to signify end of transmission                    |
| IFS (Interframe Space)         | 3 bits      | Recessive bits ('1') separating frames on the bus                      |

---

## CAN Arbitration

CAN supports multi-master communication, meaning multiple nodes can attempt to transmit at the same time. To manage this, CAN uses non-destructive arbitration, based on the message identifier.

### How It Works:

- Each bit on the CAN bus is either:<br>
   **Dominant (logical `0`)**<br>
   **Recessive (logical `1`)**

- During arbitration, nodes monitor the bus while transmitting.
- If a node sends a recessive bit but detects a dominant bit instead, it loses arbitration and immediately stops transmitting.
- The node with the lowest identifier (highest priority) wins and continues.

### Why It's Non-Destructive:

- No data is lost or corrupted.<br>
- Losing nodes can retry transmission automatically after the current message completes.

### Example:

Node A sends ID 0x100 (binary 0001 0000 0000)<br>
Node B sends ID 0x080 (binary 0000 1000 0000)<br>
→ Node B wins arbitration because it asserts a dominant 0 before Node A does.

---

## Why is CAN Considered Robust?

CAN is widely used in safety-critical systems (like automotive ECUs) because of its inherent robustness.

Key Reasons:
- Differential Signaling
→ Uses two wires (CAN_H and CAN_L), which helps reject noise and EMI (Electromagnetic Interference).

- Non-Destructive Arbitration
→ Prevents data loss even when multiple nodes transmit simultaneously.

- Error Detection & Fault Confinement
→ Multiple layers of error checking + nodes self-limit if faulty.

- Automatic Retransmission
→ Faulty frames are re-sent until acknowledged (unless node goes bus-off).

- Message Prioritization
→ Time-critical messages (like engine control) are guaranteed to get through first.

- No Clock Synchronization Needed
→ Simplifies hardware and eliminates timing drift issues seen in synchronous protocols.

---

## Error Handling in CAN

CAN has **robust error management**, built into the protocol at the hardware level. This allows nodes to detect faults, alert the network, and take corrective action automatically.


### Types of Errors Detected

| Error Type      | Description                                                                 |
|------------------|------------------------------------------------------------------------------|
| **Bit Error**     | A node sends a bit but reads a different value on the bus.                  |
| **Stuff Error**   | More than 5 consecutive identical bits are transmitted (violates bit-stuffing rule). |
| **CRC Error**     | The calculated CRC doesn't match the received CRC, indicating data corruption. |
| **Form Error**    | A field contains illegal format or reserved bit violations (e.g., EOF wrong). |
| **ACK Error**     | The transmitting node does not receive acknowledgment from any other node.  |

### Error Frames

When an error is detected, the detecting node transmits an **Error Frame**:

- Consists of **6 dominant bits** followed by **8 recessive bits** (delimiter).
- This alerts all other nodes that the current frame is invalid.
- The transmitting node will automatically **re-attempt the message** after the bus is idle.

### Fault Confinement

Each CAN node maintains two internal error counters:

- **Transmit Error Counter (TEC)**
- **Receive Error Counter (REC)**

Based on these counters, a node may enter the following states:

-  **Error Active**: Normal operation.
-  **Error Passive**: Limited capability — can still send and receive but only recessive error flags.
-  **Bus Off**: Node disconnects itself from the bus to avoid disruption. Requires software reset or power cycle to recover.

---

# Bonus: Advanced CAN Protocols

Modern embedded systems often require higher data rates or large message transfers. Standard CAN (2.0A/B) has limitations — which is where **CAN-FD** and **CAN-TP** come in.

### CAN-FD (Flexible Data-Rate)

**CAN-FD** extends the original CAN standard by enabling:

- **Faster data rates** (up to 8 Mbps)
- **Larger payloads** (up to 64 bytes vs. 8 in CAN 2.0)
- **More efficient bandwidth usage**

#### Key Features:

| Feature          | CAN 2.0         | CAN-FD               |
|------------------|------------------|------------------------|
| Max Data Length  | 8 bytes         | 64 bytes              |
| Bit Rate         | ≤ 1 Mbps        | ≤ 8 Mbps (Data Phase) |
| CRC              | 15 bits         | 17 or 21 bits         |
| Protocol ID      | ISO 11898-1     | ISO 11898-1:2015      |

- CAN-FD still uses **arbitration at 1 Mbps**, but switches to a higher **data phase bit rate** once arbitration is complete.
- Adopted in protocols like **SAE J1939-22** and high-performance automotive networks.

### CAN-TP (Transport Protocol)

**CAN-TP** is a higher-layer protocol used to **split and reassemble larger messages** over standard CAN frames (which max out at 8 bytes).

#### Why it’s needed:
- Protocols like **UDS (ISO 14229)** require multi-frame messages (diagnostics, firmware updates, etc.).
- CAN-TP manages flow control, segmentation, and reassembly.

#### Key Features:

| Layer            | Description                                |
|------------------|--------------------------------------------|
| Standard         | ISO 15765-2                                |
| Max Message Size | Up to 4 KB (or more, depending on config)  |
| Use Case         | ECU flashing, diagnostics, UDS, DoIP       |
| Frame Types      | Single Frame, First Frame, Consecutive Frame, Flow Control |

> CAN-TP is commonly used in **diagnostic stacks**, especially in automotive systems with OBD, UDS, or J1939.
