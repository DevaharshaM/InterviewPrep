# Bootloader in Embedded Systems

A **bootloader** is a small program that runs before the main firmware of an embedded system. Its job is to initialize the system, verify and load the application code, and optionally provide a way to update firmware. It acts as the **bridge between hardware reset and application execution**.

---

## Why Do We Need a Bootloader?

- To allow **firmware updates** without external programmers
- To **verify firmware integrity** (e.g., using checksum, signature)
- To support **multiple boot sources** (e.g., UART, USB, SD card)
- To enable **secure boot** features

> Without a bootloader, you'd need to reflash the chip via SWD/JTAG for any update.

---

## Bootloader Responsibilities

1. **Start after Reset**
   - Initializes clocks, memory, peripherals
2. **Checks for Valid Firmware**
   - Via checksum, CRC, magic bytes, or signature
3. **Optionally enters update mode**
   - Can wait for commands via UART/USB/OTA
4. **Jumps to main firmware**
   - Sets vector table, stack pointer, and jumps to application reset handler

---

## Memory Layout (Typical)

| Section        | Description                      |
|----------------|----------------------------------|
| 0x0800_0000    | Bootloader code (read-only)      |
| 0x0800_4000    | Application code start address   |
| RAM            | Shared for both stages           |

> The main firmware must be compiled with an offset to avoid overlapping bootloader space.

---

## Firmware Update Flow

1. User triggers update (e.g., button hold, command)
2. Bootloader enters **update mode**
3. Receives new firmware via UART/USB/OTA
4. Writes firmware to flash
5. Verifies integrity (checksum/CRC/signature)
6. Boots into the new firmware

---

## Secure Bootloaders

Secure bootloaders add protection against unauthorized firmware by:
- **Verifying signatures** (e.g., RSA/ECC-based)
- **Encrypting** firmware images
- Locking access to bootloader region

---

## Jumping from Bootloader to Application

```c
#define APP_START_ADDR 0x08004000

typedef void (*AppEntry)(void);
AppEntry app = (AppEntry)(*((uint32_t*)(APP_START_ADDR + 4)));

__set_MSP(*(volatile uint32_t*)APP_START_ADDR);
app();
```

- Sets the **Main Stack Pointer (MSP)**
- Reads the **Reset Handler** address from the vector table
- Calls the application start

---

## Bootloader Triggers

| Method         | Description                                |
|----------------|--------------------------------------------|
| GPIO Pin       | Button pressed during power-on             |
| Magic Value    | Flag stored in RAM or backup register      |
| Failed App CRC | App not valid, fall back to bootloader     |

---

## Common Bootloader Implementations

- **STM32 Bootloader (ROM-based)** – Can boot from USART, USB, CAN
- **Microchip Harmony Bootloader** – Modular and configurable
- **MCUBoot** – Open-source secure bootloader for Cortex-M
- **Custom Bootloaders** – Tailored to the application (simpler, smaller)

---

# Summary

A bootloader adds flexibility and safety to embedded firmware, especially when remote updates or security are important. Many commercial and open-source bootloaders exist, or you can build one tailored to your MCU.
