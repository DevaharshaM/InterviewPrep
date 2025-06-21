# Display Interface Comparison

Embedded systems support multiple display interfaces depending on resolution, performance, and hardware capabilities. Differences between these interfaces are shown below:

| Interface    | Type     | Pins Used | Relative Speed | Typical Resolution | MCU Friendly | Notes                                 |
|--------------|----------|-----------|----------------|--------------------|--------------|----------------------------------------|
| **I²C**      | Serial   | 2         |  Slow         | Up to 128×64       | ✅ Yes       | Mostly used for small OLEDs and LCDs   |
| **SPI**      | Serial   | 4–6       |  Moderate     | Up to 320×480      | ✅ Yes       | Popular for small TFTs and OLEDs       |
| **Parallel RGB** | Parallel | 16–28   |  Fast         | 480×272 to 800×480+| ⚠️ Limited   | Needs display controller like LTDC     |
| **MIPI-DSI** | Serial   | 5–10      |  Very Fast   | 720p, 1080p+        | ❌ No        | Used in phones, tablets, GUIs (SoC)    |
| **LVDS**     | Diff. Serial | Many   |  Very Fast   | 1080p and above    | ❌ No        | Industrial/high-end display systems    |
