# Display in Embedded Systems  

Understanding display technology is key to working with LCDs, OLEDs, and graphical interfaces in embedded systems. Some key terms used are:

---

## 1. Resolution & DPI

- **Resolution**: Number of pixels horizontally × vertically (e.g., 128×64, 320×240, 800×480)
- **DPI (Dots Per Inch)**: Pixel density; affects sharpness
  - Higher DPI = crisper image, especially on small screens

> Example: A 240×240 display at 1.3" has much higher DPI than a 320×240 display at 3.2"

## 2. Refresh Rate

- Defines **how often** the display refreshes per second (in Hz)
- Typical values: 30Hz, 60Hz, 120Hz
- Affects:
  - Smoothness of animations
  - Perceived flicker
- Higher refresh rate requires:
  - Faster communication interface (SPI, parallel)
  - More processing power

## 3. Frame Buffer

- A block of memory that holds the **entire image** to be sent to the display
- Typically organized as:
  - **Width × Height × Color depth**
- **Double buffering**: Technique to avoid screen tearing — render to one buffer while another is being sent to the display

> Example: 320×240 with RGB565 = 150 KB of framebuffer (320×240×2 bytes)

## 4. Color Formats

> **R**, **G**, **B**: Color channels (Red, Green, Blue), **A** (Alpha): Transparency channel (0 = fully transparent, 255 = fully opaque)
- **Monochrome**: 1 bit per pixel (on/off)
- **Grayscale**: 2–8 bits per pixel
- **RGB332**: 8 bits total (3 red, 3 green, 2 blue)
- **RGB565**: 16 bits total (5 red, 6 green, 5 blue)
- **RGB888**: 24 bits total (8 bits per channel)
- **RGBA / ARGB (with Alpha)**: 24 or 32 bits per pixel
- Common formats:
    - **ARGB8888**: 8 bits per channel = 32 bits total
    - **RGBA4444**: 4 bits per channel = 16 bits total

> Alpha is mostly used in **GUI rendering** (like touchscreens or overlays) and **layered interfaces**.

> RGB565 is widely used in embedded LCDs — good balance between color and memory usage

## 5. Orientation & Coordinates

- Displays often have **portrait or landscape** modes
- Origin `(0,0)` is typically:
  - Top-left for most displays
  - Configurable via software (some drivers flip/mirror)

## 6. Drawing Methods

- **Pixel-by-pixel**: Useful for animations and custom shapes
- **Block transfers (blitting)**: Write a region or whole frame at once
- **Character modes**: Some simple displays (like 16x2 LCD) use fixed fonts

---

# Summary

| Concept       | Description                            |
|---------------|----------------------------------------|
| Resolution    | Pixel dimensions (e.g., 320×240)       |
| Refresh rate  | Updates per second (Hz)                |
| Framebuffer   | Memory storing current screen image    |
| Color depth   | Bits per pixel (e.g., RGB565 = 16bpp)  |
| DPI           | Pixel density; affects sharpness       |
