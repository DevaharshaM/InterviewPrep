# Polling vs Interrupts in Embedded Systems

Polling and interrupts are two methods used to **detect and respond to events** in embedded systems, such as a button press, data arrival, or a timer overflow.

---

## Polling

In polling, the CPU **continuously checks** (or "polls") a peripheral or status register in a loop.

### Characteristics:
- **Blocking**: CPU is occupied until event occurs.
- **Predictable**: Easy to implement and debug.
- **Inefficient**: Wastes CPU cycles if no event is pending.

### Example:
```c
while (1) {
  if (UART_Ready()) {
    char c = UART_Read();
    // process data
  }
}
```

## Interrupts

In interrupt-driven systems, the CPU executes other tasks until the peripheral signals an event via an interrupt. The CPU then pauses its work to handle it.

### Characteristics:
- **Efficient**: CPU can sleep or do other work until needed.
- **Asynchronous**: Responds only when events occur.
- **Requires ISR**: A handler function is triggered when interrupt occurs.

### Example:
```c
void USART1_IRQHandler(void) {
  char c = USART_Read();
  // process character
}
```

## Polling vs Interrupts

| Feature          |	Polling	                    | Interrupts                         |
|------------------|------------------------------|------------------------------------|
| CPU Utilization  |	High (wasted cycles)        |	Low (only wakes when needed)       |
| Response Time	   | Can be delayed (loop time)   | Immediate (ISR triggered)          |
| Complexity       |	Low	                        | Medium (ISR management needed)     |
| Use Case         |	Fast-check, real-time loops |	Asynchronous events, low-power MCUs|

## When to Use What?

- Polling:<br>
o When the event occurs frequently and predictably<br>
o Simpler logic or in systems without interrupts<br>
o Very time-critical polling (e.g., ultra-fast ADC sampling)

- Interrupts:<br>
o When power saving is important (CPU can sleep)<br>
o For asynchronous or rare events (e.g., button press)<br>
o In multitasking or time-shared systems

>  In practice, many systems use a combination: polling for time-critical tasks, interrupts for asynchronous events.

---

# Interrupt Service Routines (ISR) 

An **Interrupt Service Routine (ISR)** is a special function that is **executed automatically** in response to an interrupt signal from hardware or a peripheral.

When an interrupt occurs:
1. The current program execution is paused.
2. The corresponding ISR is executed.
3. The program resumes from where it left off.

---

## Key Properties of ISRs

- **No return value**: ISRs are typically declared `void`.
- **Cannot take arguments**
- **Should execute quickly**: Long ISRs block other interrupts or tasks.
- **Registers & flags may need manual clearing**, depending on the hardware.
- **Interrupt flags must often be cleared in the ISR**, or it may retrigger endlessly.
