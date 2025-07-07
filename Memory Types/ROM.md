# ROM in Embedded Systems

**ROM (Read-Only Memory)** is a type of **non-volatile memory** used to **store data permanently**. In embedded systems, it typically holds firmware or program code that should not be lost when power is off.

---

## Key Features

| Feature           | Description                                        |
|------------------|----------------------------------------------------|
| **Non-Volatile** | Retains data without power                         |
| **Read-Mostly**  | Some types allow limited write/erase capabilities  |
| **Used For**     | Firmware, bootloader, lookup tables, constants     |

---

## Types of ROM

### 1. **Masked ROM**

- Programmed during chip fabrication
- **Inflexible**: Cannot be altered after manufacturing
- **Used in**: High-volume production with stable firmware

---

### 2. **PROM (Programmable ROM)**

- Initially blank and can be programmed **once**
- **Fuses** inside chip are burned to store data
- **Used in**: Legacy systems or when small batch programming is acceptable

---

### 3. **EPROM (Erasable Programmable ROM)**

- Can be erased using **UV light** and reprogrammed
- Transparent quartz window is used for exposure
- **Slower and less durable** than EEPROM
- **Obsolete** in most modern systems

---

### 4. **EEPROM (Electrically Erasable PROM)**

- Can be electrically erased and rewritten **byte by byte**
- Slower than Flash memory but highly **flexible**
- **Used in**: Storing calibration data, configuration, MAC addresses

---

## Common Use Cases of ROM in Embedded Systems

| Component        | ROM Role                            |
|------------------|--------------------------------------|
| Bootloader       | Stored in ROM/Flash for startup      |
| Microcontroller  | Internal ROM for program code        |
| Configuration    | Permanent values like serial numbers |
| Lookup Tables    | Fixed tables like sin/cos values     |

---

## Is Flash also ROM?

Yes — Flash is a modern, rewritable type of **ROM** that balances **non-volatility** with **rewritability**. It is commonly used for program memory in microcontrollers and often considered a **subset of ROM**.

---

# Summary

- ROM is essential for storing **permanent or semi-permanent** code/data.
- Modern embedded systems use **EEPROM** and **Flash** instead of PROM/EPROM.
- Type selection depends on how often updates are required and cost constraints.
