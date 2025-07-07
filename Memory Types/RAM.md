# RAM in Embedded Systems

**RAM (Random Access Memory)** is a type of **volatile memory** used for **temporary data storage** during the execution of programs in embedded systems. It is essential for holding variables, buffers, and stack/heap data.

---

## Characteristics

| Property         | Description                               |
|------------------|-------------------------------------------|
| **Volatile**     | Loses data when power is lost             |
| **Read/Write**   | Supports both operations dynamically      |
| **Fast Access**  | Faster than most non-volatile memories    |
| **Random Access**| Any memory location can be accessed directly |

---

## Where is RAM used?

- **Stack**: Local variables, function calls
- **Heap**: Dynamic memory allocation
- **Buffers**: Data transmission/reception (e.g., UART, SPI)
- **Framebuffers**: For displays and graphics
- **Temporary storage**: While processing sensor data, etc.

---

## RAM Types

### 1. **SRAM (Static RAM)**

| Feature     | Detail                                       |
|-------------|----------------------------------------------|
| No Refresh  | Data is retained as long as power is on      |
| Speed       | Very fast                                    |
| Cost        | Expensive per bit                            |
| Use Case    | Caches, small on-chip memory in MCUs         |

---

### 2. **DRAM (Dynamic RAM)**

| Feature     | Detail                                       |
|-------------|----------------------------------------------|
| Requires Refresh | Needs periodic refreshing to hold data |
| Speed       | Slower than SRAM                            |
| Cost        | Cheaper and denser than SRAM                |
| Use Case    | Large off-chip memory in advanced systems   |

---

### 3. **SDRAM (Synchronous DRAM)**

| Feature     | Detail                                       |
|-------------|----------------------------------------------|
| Clocked     | Operates in sync with system clock           |
| Burst Access| Can read/write multiple words in sequence    |
| Use Case    | External memory in high-speed applications   |

---

### 4. **LPDRAM (Low Power DRAM)**

| Feature     | Detail                                       |
|-------------|----------------------------------------------|
| Power Saving| Optimized for mobile/portable applications   |
| Sleep Modes | Supports deep sleep and refresh reductions   |
| Use Case    | Wearables, battery-powered embedded systems  |

---

# Summary

- **SRAM** is used inside microcontrollers for its speed and simplicity.
- **DRAM/SDRAM** is used in higher-end systems needing more memory.
- **LPDRAM** is ideal for low-power battery-based embedded systems.

Choosing the right RAM depends on your system’s **performance, power, and cost** requirements.
