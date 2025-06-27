# Toggle a Specific Bit in an Integer

---

This program toggles (flips) the **k-th bit (0-indexed from LSB)** of a given number using bitwise XOR.

### Example:
- Input: 10 (Binary: 00001010)
- Toggle bit at position 1 → Result: 8 (Binary: 00001000)

---

## Code

```c
/* include required header files */
#include <stdio.h>
#include <stdint.h>

/* main function */
int main()
{
    uint32_t u32_num = 10, u32_bitPos = 0, u32_res = 0;
    
    printf("Enter the bit position:");
    scanf("%d", &u32_bitPos);
    u32_res = u32_num ^ (1 << u32_bitPos);
    printf("The result after bit reversal is: %d", u32_res);
    
    return 0;
}
```

**Time Complexity**: `O(1)`<br>
**Space Complexity**: `O(1)`
