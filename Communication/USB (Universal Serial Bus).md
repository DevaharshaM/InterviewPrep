# USB (Universal Serial Bus)

USB is one of the most widely adopted communication standards in embedded systems and consumer electronics. It enables communication between a host (usually a PC or microcontroller) and peripheral devices like keyboards, flash drives, cameras, or microcontrollers.

---

## Topology and Roles

- **Host**: Controls communication, initiates data transfer
- **Device**: Responds to host requests
- **Hubs**: Allow multiple devices to connect to a single USB port (tree topology)

Each device gets a **unique address** assigned during enumeration.

---

## USB Transfer Types

| Type         | Use Case                     | Speed      | Reliability | Example                        |
|--------------|-------------------------------|------------|-------------|--------------------------------|
| Control      | Device configuration          | Low        | High        | Enumeration, standard commands |
| Bulk         | Large, non-time-critical data | High       | High        | File transfers (USB drives)    |
| Interrupt    | Small, fast, regular packets  | Medium     | High        | Mouse, keyboard                |
| Isochronous  | Continuous, time-sensitive    | Medium/High| No Retry    | Audio/Video streaming          |

---

## USB Descriptors

USB devices describe themselves using a hierarchy of descriptors:

- **Device Descriptor**: Overall information (Vendor ID, Product ID, USB version)
- **Configuration Descriptor**: Power and interface layout
- **Interface Descriptor**: Defines a logical function (e.g., HID, CDC)
- **Endpoint Descriptor**: Describes the data flow channels

These are communicated during **enumeration** when a device is first connected.

---

## Endpoints and Pipes

- **Endpoint**: Logical data source/sink on a device
- **Pipe**: Logical communication link between host software and endpoint

Each endpoint has:
- **Address** (number)
- **Direction**: IN (to host) or OUT (from host)
- **Transfer type** (control, bulk, etc.)

Example: `Endpoint 1 IN` could be a CDC TX channel.

---

## USB Classes (Device Types)

USB supports standard **device classes** that allow operating systems to load generic drivers.

| Class | Description               | Example Devices             |
|-------|---------------------------|-----------------------------|
| CDC   | Communication (Serial)    | Virtual COM Port (e.g. STM32 USB CDC)
| HID   | Human Interface Device    | Mouse, Keyboard, Gamepad    |
| MSC   | Mass Storage Class        | USB Flash Drives            |
| UVC   | Video Class               | Webcams                     |
| Audio | Audio Streaming           | Headsets, Microphones       |

---

## USB Versions

| Version | Speed        | Max Data Rate   | Common Connectors       |
|---------|--------------|------------------|--------------------------|
| 1.1     | Low/Full     | 1.5 Mbps / 12 Mbps| Type-A, Type-B          |
| 2.0     | High         | 480 Mbps         | Type-A, Mini-B, Micro-B  |
| 3.x     | SuperSpeed   | 5–10+ Gbps       | Type-A, Type-C           |
| 4.0     | Thunderbolt  | 40 Gbps          | Type-C                   |

---

## USB Connector Pinouts

The most commonly used USB connectors and their pin functions:

<figure>
 <img src = " ">
 <figcaption>Figure 1: Commonly used USB pins</figcaption>
</figure>

### USB Type-A / Type-B / Micro-B (USB 2.0)

| Pin | Name | Function                          |
|-----|------|-----------------------------------|
| 1   | VBUS | +5V Power Supply                  |
| 2   | D-   | Differential Data Line (-)        |
| 3   | D+   | Differential Data Line (+)        |
| 4   | GND  | Ground                            |
| 5   | ID   | (Micro-B only) OTG Role Detection |

> **ID Pin**:
> - Floating → device acts as a **peripheral**  
> - GND → device acts as a **host**

### USB Type-C (USB 2.0 / 3.x / PD)

| Pin        | Name      | Function                                  |
|------------|-----------|-------------------------------------------|
| A1, B12    | GND       | Ground                                    |
| A4, B9     | VBUS      | +5V to +20V (Power Delivery)              |
| A6, A7     | D+, D-    | USB 2.0 Differential Data Lines           |
| B6, B7     | D+, D-    | (Symmetrical for reversible connection)   |
| A5, B5     | CC1, CC2  | Configuration Channel (cable detection, orientation) |
| A2, A3     | TX+ / TX- | Superspeed transmit                      |
| B10, B11   | RX+ / RX- | Superspeed receive                       |
| B2, B3     | TX+ / TX- | (Reversible pairs)                        |
| A10, A11   | RX+ / RX- | (Reversible pairs)                        |
| A8, B8     | SBU1, SBU2| Sideband Use (Audio Accessory, Debug)    |

> ⚠️ Not all Type-C pins are used in basic USB 2.0-only implementations.

---

# Summary

USB is a powerful, flexible protocol with support for:
- Multiple device types (HID, storage, serial)
- Structured communication via descriptors and endpoints
- Simple power + data over a single cable

Its wide adoption makes it critical for embedded developers building user-facing or data-driven systems.

---
