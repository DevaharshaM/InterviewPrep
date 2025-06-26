# Check if a Number is a Power of 2

---

This program checks whether a given **non-negative integer** is a power of 2.

### Examples:
- `8` → ✅ Power of 2 (2³)
- `14` → ❌ Not a power of 2
- `1` → ✅ Power of 2 (2⁰)
- `0` → ❌ Not a power of 2

---
## Code

```c
/* include required header files */
#include <stdio.h>
#include <stdbool.h>

/* main function */
int main()
{
    int num = 8;
    
    if((num != 0) && ((num & (num-1)) == 0))
    {
        printf("Given number is a power of 2");
    }
    else
    {
        printf("Given number is not a power of 2");
    }
    
    return 0;
}
```
## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(1)`<br>
**Space Complexity**: `O(1)`
