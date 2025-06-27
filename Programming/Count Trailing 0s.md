# Count Number of Trailing Zeros in Binary Representation

---

This program counts the number of **consecutive 0s starting from the Least Significant Bit (LSB)** until the first 1 appears in the binary representation of a number.

### Example:  
- 6 → Binary: 00000110 → Trailing 1s: **1**
- 8 → Binary: 00001000 → Trailing 0s: **3**
- 7 → Binary: 00000111 → Trailing 0s: **0**

---

> Assumes the number is an 8-bit unsigned integer.

```c
/* include required header files */
#include <stdio.h>
#include <stdint.h>

/* main function */
int main()
{
    uint8_t u8_num = 6, u8_cntZeros = 0;

    if (u8_num == 0)
        u8_cntZeros = 8;
    else
    {
        while (!(u8_num & 1))
        {
            u8_cntZeros++;
            u8_num = u8_num >> 1;
        }
    }

    printf("Given number has %d trailing zeroes before first occurrence of 1", u8_cntZeros);

    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(log n) (worst-case n is all 0s except the MSB)`<br>
**Space Complexity**: `O(1)`

