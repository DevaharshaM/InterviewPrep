# Communication Protocols Comparison

Embedded systems support multiple communication protocols depending on speed, cable length, and hardware capabilities. Differences between these protocols are shown below:

| Feature            | UART              | SPI               | I2C               | CAN                        | USB                        |
|--------------------|-------------------|--------------------|--------------------|-----------------------------|-----------------------------|
| Type               | Serial            | Serial             | Serial             | Serial (Bus)               | Serial                      |
| Sync/Async         | Asynchronous      | Synchronous        | Synchronous        | Asynchronous                | Async + Sync                |
| Duplex             | Full              | Full               | Half               | Half                        | Half (polling)             |
| Master-Slave       | Point-to-point    | Master-Slave       | Multi-Master       | Multi-Master                | Host-Device                 |
| Multi-device       | ❌                | Limited (1:M)      | ✅ (7-bit addr)     | ✅                          | ✅ (via hub)                |
| Speed Range        | Up to ~1 Mbps+    | Up to ~50 Mbps+    | Up to 3.4 Mbps     | Up to 1 Mbps (2.0), 5 Mbps (FD) | 1.5 Mbps to 40 Gbps    |
| Clock Line         | ❌                | ✅ (SCLK)           | ✅ (SCL)            | ❌                          | Optional (for sync)         |
| Data Lines         | TX, RX            | MOSI, MISO         | SDA                | CAN_H, CAN_L                | D+, D-                      |
| Addressing         | ❌                | ❌                 | ✅ (7/10 bit)       | ✅ (Message ID-based)       | ✅ (Descriptors & IDs)      |
| Error Handling     | Basic (parity)    | Manual (SW-based)  | Basic ACK/NACK     | Advanced (error counters, arbitration) | Protocol-managed   |
| Arbitration        | ❌                | ❌                 | Clock stretching    | Non-destructive arbitration | Host-managed                |
| Hardware Complexity| Very Low          | Low                | Medium             | Medium-High                 | High                        |
| Cable Length       | Short             | Very Short         | Short-Medium       | Long (up to 40m)            | Short-Medium                |
| Typical Use        | Debug console, GPS| Flash, sensors     | EEPROM, RTC, IO expanders | Automotive, industrial   | Peripherals, flash drives   |
