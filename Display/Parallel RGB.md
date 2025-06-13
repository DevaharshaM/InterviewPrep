# Parallel RGB Interface (DPI / TTL)

The **Parallel RGB** interface, often called **DPI (Display Pixel Interface)** or **TTL interface**, is a widely used method for sending pixel data from a microcontroller or display controller to an LCD or TFT panel.

It transmits **pixel data in parallel** — one pixel per clock cycle — along with sync signals that coordinate when and how pixels should be displayed.

---

## Key Characteristics

| Feature         | Description                        |
|-----------------|------------------------------------|
| Data Transfer   | Parallel (RGB888, RGB565, etc.)    |
| Interface Type  | Unidirectional                     |
| Clock           | Pixel Clock (PCLK)                 |
| Sync Signals    | VSYNC, HSYNC, DE                   |
| Resolution      | Medium to High                     |
| MCU Support     | STM32 (LTDC), some LPC, i.MX, etc. |

---

## Basic Signal Lines

### 1. **Data Bus**
- Typically **16-bit (RGB565)** or **24-bit (RGB888)**.
- RGB data is sent simultaneously using dedicated lines per bit.

### 2. **PCLK (Pixel Clock)**
- Each rising edge transfers one pixel.
- Must match the display’s pixel frequency requirements.

### 3. **HSYNC (Horizontal Sync)**
- Marks the end of each row.
- Used by the display to move to the next line.

### 4. **VSYNC (Vertical Sync)**
- Marks the end of a frame.
- Tells the display to start rendering the next frame from the top row.

### 5. **DE (Data Enable)**
- High only when valid pixel data is being sent.
- Gates the pixel transmission window within each line.

---

## Parallel RGB Wiring Diagram

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Display/blockParallel.png">
 <figcaption>Figure 1: Parallel RGB888 Interface</figcaption>
</figure>

---

## Timing Description

In a Parallel RGB display, the pixel and frame timing is coordinated using a combination of `PCLK`, `DE`, `HSYNC`, and `VSYNC`:

- **PCLK**: Transfers one pixel on each rising edge.
- **DE**: Goes HIGH during the active region of each row — gates valid pixel data.
- **HSYNC**: Goes LOW at the end of each line — moves to the next row.
- **VSYNC**: Goes LOW at the end of each frame — triggers the start of a new frame.

---

## Frame Transmission Flow

| Step | Signal      | State         | Description                         |
|------|-------------|---------------|-------------------------------------|
| 1    | VSYNC       | LOW pulse     | Start of new frame                  |
| 2    | HSYNC       | LOW pulse     | Start of a new row                  |
| 3    | DE          | HIGH          | Active video region begins          |
| 4    | PCLK        | Rising edges  | Each pixel transferred per edge     |
| 5    | DE          | LOW           | End of active pixels in this row    |
| 6    | HSYNC       | Next row      | Next line transmission starts       |
| 7    | VSYNC       | After last row| Frame ends, VSYNC triggers restart  |

---

## Advantages

- High-speed: One pixel per clock cycle.
- No protocol overhead: Raw pixel stream.
- Ideal for medium-to-high resolutions (up to 800×480, even 1280×800).
- Supported directly by LTDC or external display controllers.

## Limitations

- Many GPIOs required (16–24 data + 3–4 control).
- Tight timing: Requires precise pixel clock and sync generation.
- Difficult to extend over long distances due to EMI.
- Not supported by all microcontrollers.
