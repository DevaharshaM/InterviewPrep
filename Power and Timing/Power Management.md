# Power Management in Embedded Systems

Power management is a critical aspect of embedded system design — especially in battery-powered, portable, or always-on applications. It ensures that the system operates reliably, efficiently, and within thermal and energy constraints.

---

## 1. Power-On Reset (POR)

**Power-On Reset** ensures that a microcontroller or processor starts in a **known state** when power is first applied.

### Key Points:
- Triggered when Vcc rises above a safe threshold.
- Prevents the system from executing **garbage instructions** during unstable power.
- Often integrated in microcontrollers — no external circuitry needed.

> Think of POR as the system’s first safety check during power-up.

---

## 2. Brown-Out Reset (BOR)

**Brown-Out Reset** monitors the **supply voltage** during operation. If it dips below a preset threshold, the system is reset to avoid erratic behavior.

### Why It's Important:
- Voltage dips can cause corruption of SRAM or flash.
- BOR ensures the system doesn’t operate **below safe voltage levels**.
- Often configurable in MCUs (e.g., STM32 allows BOR threshold selection).

> System auto-reboots when voltage returns to safe levels.

---

## 3. Low Power Modes (Sleep & Standby)

To extend battery life or reduce heat, microcontrollers offer multiple **low power modes**. These shut down parts of the system not currently needed.

### Common Modes:

| Mode         | CPU | Peripherals | Wake-Up Time | Power Consumption |
|--------------|-----|-------------|---------------|--------------------|
| **Sleep**    | Off | On          | Fast          | Low                |
| **Stop**     | Off | Most Off    | Medium        | Lower              |
| **Standby**  | Off | Off         | Slow          | Very Low           |

> Some MCUs support **deep sleep** or **backup modes** with sub-µA current draw.

---

## 4. Voltage Regulation and LDOs

Voltage regulators ensure that components receive a **stable and clean voltage** supply.

- **LDO (Low Dropout Regulator)**: Common in MCUs for generating internal 1.8V/3.3V rails.
- A good regulator is essential for **reliable POR/BOR** operation.

> A noisy or unstable regulator can lead to unexpected resets.

---

## 5. Dynamic Voltage and Frequency Scaling (DVFS)

DVFS allows the system to reduce **clock speed** and **core voltage** during low workload periods to save power.

- More common in **SoCs** and advanced MCUs (e.g., ARM Cortex-A).
- Requires **voltage scaling support** in both hardware and firmware.

> Lower frequency = lower dynamic power (P ∝ V²f)

---

## 6. Battery Monitoring

Embedded systems that rely on battery power must monitor voltage levels to:

- Warn the user
- Shut down safely
- Trigger **battery-saving modes**

### Methods:
- ADC-based battery level sensing
- Dedicated battery monitor ICs
- Voltage comparator + interrupt

---

## 7. Power Domains and Gating

Some MCUs and SoCs divide internal logic into **power domains**:

- **Always-On Domain** (RTC, wake-up logic)
- **Main Domain** (CPU, RAM, peripherals)

Power gating allows turning off unused domains to reduce leakage.

> Example: A sensor hub may remain on while the CPU sleeps.

---

## 8. Wake-Up Sources

When in low-power modes, the system must be able to **wake up** based on:

- **GPIO interrupt** (e.g., button press)
- **RTC alarm** (e.g., every 10 seconds)
- **Timer overflow**
- **Communication events** (USART, CAN, I2C)

These are configured via **interrupts**, and must be routed through **low-power I/O domains**.

---

## Summary

| Feature               | Purpose                                 |
|------------------------|-----------------------------------------|
| **POR**               | Resets system on power-up               |
| **BOR**               | Protects during low voltage             |
| **Low Power Modes**   | Reduce current draw during idle         |
| **DVFS**              | Adjusts performance for power savings   |
| **Battery Monitoring**| Ensures safe shutdown                   |
| **Power Gating**      | Disables unused modules                 |
| **Wake-Up Sources**   | Bring system back to active mode        |

---

# Bonus: Watchdog Timer 

While not strictly a power management feature, the **Watchdog Timer (WDT)** is often used alongside BOR/POR for system safety.

- If the MCU hangs due to voltage instability or software bugs, WDT can reset it.
- Acts as a **self-recovery mechanism**.

*You can read more in the dedicated [Watchdog Timer section].*
