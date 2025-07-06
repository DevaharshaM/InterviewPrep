# Memories in Embedded Systems

In embedded systems, memory is a fundamental component used to store code, data, and temporary variables. Understanding different types of memory helps in designing efficient and reliable systems.

---

## Classification of Memory

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Memory%20Types/memory.png">
  <figcaption>Figure 1: Memory Classification</figcaption>
</figure>

---

## RAM (Random Access Memory)

- **Volatile**: Loses data when power is lost.
- **Used for**: Temporary storage like stack, heap, buffers, etc.

| Type     | Description |
|----------|-------------|
| **SRAM** (Static RAM) | Faster, no refresh needed, used for caches and small buffers |
| **DRAM** (Dynamic RAM) | Needs refreshing, denser and cheaper than SRAM |
| **SDRAM** (Synchronous DRAM) | DRAM that works in sync with CPU clock |
| **LPDRAM** (Low-Power DRAM) | Optimized DRAM for low power consumption in portable systems |

---

## ROM (Read Only Memory)

- **Non-volatile**: Retains data after power off.
- **Used for**: Firmware and fixed program storage.

| Type         | Description |
|--------------|-------------|
| **PROM**     | Programmable once after manufacturing |
| **EPROM**    | Erasable using UV light and reprogrammable |
| **Masked ROM** | Programmed during manufacturing; can't be altered |

---

## Hybrid Memory (Non-Volatile + Writable)

These memories combine non-volatility with reprogrammability. Commonly used for configuration data, firmware updates, etc.

| Type         | Description |
|--------------|-------------|
| **EEPROM**   | Electrically erasable and rewritable; byte-wise access |
| **Flash**    | Fast, block-wise erasable; used in SD cards, USBs |
| **NVRAM**    | Non-volatile RAM with battery backup or special tech |

### Flash Variants:
| Type | Description |
|------|-------------|
| **NOR**  | Faster read, supports execute-in-place (XIP), used for firmware |
| **NAND** | Denser, cheaper, faster write/erase cycles, used for storage |
