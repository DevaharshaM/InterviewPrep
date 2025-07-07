# Memory Type Comparison – Embedded Systems

Embedded systems use different memory types for different roles — volatile memory for runtime data and non-volatile memory for persistent code and configuration storage.

This section compares the key characteristics of **RAM**, **ROM**, and **Hybrid memory types** (like Flash, EEPROM, NVRAM) in embedded applications.

---

## Memory Comparison Table

| Feature             | RAM                       | ROM                        | Hybrid Memory                  |
|---------------------|---------------------------|-----------------------------|--------------------------------|
| **Volatility**       | Volatile                  | Non-volatile                | Non-volatile                   |
| **Programmability**  | Read/Write                | Write-once (factory/masked)| Reprogrammable (electrically) |
| **Write Granularity**| Byte or word              | N/A                         | Byte (EEPROM), Block (Flash)  |
| **Speed**            | Fast (SRAM), Medium (DRAM)| Fast (read)                 | Moderate                       |
| **Usage**            | Stack, heap, runtime data | Boot code, fixed firmware   | Firmware, config, logs        |
| **Endurance**        | Unlimited                 | Unlimited                   | Limited (10⁴–10⁶ cycles)      |
| **Retention**        | No                        | Yes                         | Yes                            |
| **Examples**         | SRAM, DRAM, SDRAM         | Mask ROM, PROM, EPROM       | EEPROM, NOR/NAND Flash, FRAM  |
