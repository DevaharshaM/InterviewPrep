# Data Type Sizes in C

In C, each data type occupies a certain amount of memory, and this size can depend on the architecture (e.g., 32-bit vs 64-bit), compiler, and platform. Understanding these sizes is crucial in systems programming, embedded development, and when optimizing memory usage.

---

## Common Data Type Sizes

### On a 32-bit OS -

| Data Type | Typical Size (bytes) |
|-----------|----------------------|
| `char`    | 1                    |
| `short`   | 2                    |
| `int`     | 4                    |
| `long`    | 4                    |
| `float`   | 4                    |
| `double`  | 8                    |
| `pointer` | 4                    |

### On a 64-bit OS -

| Data Type | Typical Size (bytes) |
|-----------|----------------------|
| `char`    | 1                    |
| `short`   | 2                    |
| `int`     | 4                    |
| `long`    | 8                    |
| `float`   | 4                    |
| `double`  | 8                    |
| `pointer` | 8                    |

> Note: The size of `int` often stays 4 bytes even on 64-bit systems for compatibility.

---

## Using `sizeof()` in C

C provides the `sizeof` operator to check the size of any data type or variable:

```c
#include <stdio.h>

int main() {
    printf("Size of int: %zu\n", sizeof(int));
    printf("Size of pointer: %zu\n", sizeof(void*));
    return 0;
}
```

---

## Why Size Knowledge Matters (Especially in Embedded Systems)

- Memory is limited in embedded systems — knowing exact sizes helps avoid over-allocation.
- Aligning data properly can avoid bus faults and improve performance.
- Helps in memory-mapped I/O, where you must match register size and layout exactly.
- Required when interfacing with hardware or protocols that expect specific byte sizes.

---

## Fixed-Width Types: using <stdint.h>

To ensure portability and clarity, C provides fixed-width integer types in <stdint.h>:

| Type	     | Description             |
|------------|-------------------------|
| `uint8_t`  | Unsigned 8-bit integer  |
| `int16_t`	 | Signed 16-bit integer   |
| `uint32_t` | Unsigned 32-bit integer |
| `int64_t`  | Signed 64-bit integer   |

These are especially useful when:

- Writing cross-platform code
- Defining exact-sized data in protocols or hardware registers
- Avoiding surprises caused by varying int, long, etc. sizes
