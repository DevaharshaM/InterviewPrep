# Timers in Embedded Systems

Timers are fundamental peripherals in embedded systems. They allow the microcontroller to **measure time**, **generate delays**, **create waveforms**, and respond to periodic or edge-based events — all with minimal CPU involvement.

Timers typically use the system clock (or a divided version of it) to increment an internal counter, triggering actions when specific conditions are met.

---

## Timers vs Counters

| Feature        | Timer (Internal Clock)      | Counter (External Input)      |
|----------------|------------------------------|-------------------------------|
| Source         | Internal system/peripheral clock | External events (e.g., GPIO edges) |
| Use case       | Delays, scheduling, PWM      | Event counting, frequency measurement |

> In most microcontrollers, a single hardware block can often be configured as either a **timer** or a **counter**.

---

## 1. Compare Mode

In Compare mode, the timer continuously counts up (or down), and an **event is triggered** when the counter value **matches a predefined compare value**.

Use Cases:
- Generating periodic interrupts (e.g., 1ms system tick)
- Toggling a pin for square wave generation
- Delayed start of a function

```c
if (TIMx->CNT == TIMx->CCR1) {
  // Compare match logic
}
```

## 2. Capture Mode

Capture mode allows the timer to store its counter value when an external signal (e.g., rising or falling edge) occurs on a capture pin.

Use Cases:
- Measuring the frequency of a signal
- Pulse width measurement
- Timing external events

```c
void TIMx_IRQHandler() {
  if (TIMx->SR & TIM_SR_CC1IF) {
    uint16_t captured_value = TIMx->CCR1;
    // Use captured value
  }
}
```

## 3. PWM (Pulse Width Modulation)

PWM uses timer compare logic to generate a repeating waveform where the duty cycle (ON time) can be controlled.

Use Cases:
- Controlling motor speed
- Dimming LEDs
- DAC-like analog outputs

```c
TIMx->CCR1 = duty_cycle_value;  // t_duty = ((t_on + t_off) / t_period) * 100
```

<figure>
  <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/microController/Power%20and%20Timing/pwm.png">
  <figcaption>Figure 1: PWM generation</figcaption>
</figure>

---

# Bonus: Other Timer modules

## Watchdog Timer (WDT)

- A hardware timer that resets the microcontroller if the software fails to operate correctly — usually due to a lockup, infinite loop, or unexpected delay.
- Protects against software hangs or stuck loops.

## SysTick (System Timer)

- A dedicated 24-bit countdown timer on ARM Cortex-M cores.
- Often used to create a 1ms periodic interrupt in bare-metal or RTOS applications.

## Real-Time Clock (RTC)

- A low-power timer used for long-term timekeeping.
- Usually runs on an external 32.768 kHz crystal.
- Can operate in standby modes and retain time with battery backup.
