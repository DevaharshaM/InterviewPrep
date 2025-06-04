# Type Qualifiers in C

In C, **type qualifiers** modify the behavior of variables. They tell the compiler about how that variable should be treated.

The two most common qualifiers are:

- `const`
- `volatile`

---

## const keyword

A `const` variable means **“the value cannot be changed”**. Once the variable is declared with the `const` keyword, the compiler treats it as read-only. The value cannot be modified after initialization.

### Example:

```c
const int max_limit = 100;
max_limit = 200; // ❌ Error: assignment of read-only variable
```
### Why use const?

- Prevents accidental modification
- Enables compiler optimizations
- Improves code readability and intent

## volatile keyword

A `volatile` variable means **the value can change unexpectedly**. This tells the compiler that the value might be altered outside the current code (e.g., by hardware or an ISR), so it must always reload it from memory.

### Example:

```c
volatile int flag = 0;

void ISR() {
    flag = 1; // Changed by an interrupt
}

int main() {
    while (flag == 0);  // ✅ With volatile, the compiler reloads 'flag' every time
}
```

### When to use volatile?

- Variables modified inside Interrupt Service Routines (ISRs)
- Accessing hardware registers
- Variables shared across multiple threads/tasks

---

## Advanced Example

Let’s take a look at this example:

### Example:

```c
#include <stdio.h>

#define HW_REG_ADDR 0x4000
const volatile int *uart_status = (int *) HW_REG_ADDR;

void check_uart_status() {
    if (*uart_status & 0x01) {
        printf("UART transmit buffer is empty.\n");
    } else {
        printf("UART is busy.\n");
    }
}
```

Here, *uart_status* is a pointer to a memory-mapped hardware register at address 0x4000. The use of `const volatile` means that the value of *uart_status* is a constant i.e. the program cannot modify the value but can be changed by the external pin or by the hardware.
This combination is common when dealing with status or read-only hardware registers that are updated by the peripheral or an interrupt source.