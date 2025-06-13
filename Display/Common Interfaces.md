# Display Interfaces – SPI, I²C, and LVDS

Embedded systems utilize various interfaces to communicate with displays, depending on the resolution, speed, and cost. Three common serial interfaces are: 
- **SPI**
- **I²C**
- **LVDS**.

---

## 1. SPI-Based Displays

SPI (Serial Peripheral Interface) is commonly used for small to medium-sized displays like OLEDs and TFT LCDs.

### Common Controllers
- ST7735, ILI9341, SSD1306, ST7789

### Interface Pins
- MOSI – Master Out Slave In
- SCLK – Clock
- CS – Chip Select
- D/C – Data/Command
- Optional: RST (Reset), BL (Backlight)

### Behavior
- Data and commands are sent serially on the same line (MOSI).
- The D/C pin distinguishes between command and data.
- Pixel data is often sent in formats like RGB565.
- Larger framebuffers can be transmitted using DMA for better speed.

> Common resolutions: 128×160, 240×320, 320×480

---

## 2. I²C-Based Displays

I²C is ideal for low-resolution, low-bandwidth displays, often used in power-sensitive or minimal-wire applications.

### Common Controllers
- SSD1306, SH1106, PCF8574 (for HD44780 character LCDs)

### Interface Pins
- SDA – Data
- SCL – Clock

### Behavior
- Each display has an I²C address (e.g., 0x3C).
- Control byte indicates command (`0x00`) or data (`0x40`).
- Typically limited to monochrome or small displays.
- Data rate is much lower than SPI.

> Common sizes: 128×32, 128×64

---

## 3. LVDS – Low-Voltage Differential Signaling

LVDS is a high-speed, low-noise interface used for larger displays and high resolutions. It uses differential signaling over multiple lanes.

### Use Cases
- Laptop displays, industrial screens, single-board computers
- Not directly supported by microcontrollers — requires bridge ICs or native LVDS in SoCs

### Characteristics
- Capable of carrying high-speed pixel data across longer cables
- Often used in conjunction with backlight drivers and touch controllers
- Used when resolution exceeds what SPI/I²C/Parallel interfaces can handle

---

# Summary

| Interface | Use Case                 | Speed      | Pins  | Ideal Resolution | Notes                              |
|-----------|--------------------------|------------|-------|------------------|-------------------------------------|
| **SPI**   | Small TFT, OLED          | Medium     | 4–6   | up to 320×480    | Requires D/C line for control/data  |
| **I²C**   | OLED, character LCDs     | Low        | 2     | up to 128×64     | Very simple, limited bandwidth      |
| **LVDS**  | Large industrial displays| Very High  | Many  | 7"+, HD displays | Needs bridge or SoC integration     |
