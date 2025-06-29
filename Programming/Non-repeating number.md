# Find the Only Non-Repeating Element in an Array

---

This program finds the **only unique element** in an array where **all other elements appear exactly twice**, using bitwise XOR.

### Example:
- Input: `[2, 3, 5, 4, 5, 3, 4]`
- Output: `2`

---

## Code

```c
/* include required header files */
#include <stdio.h>

/* main function */
int main()
{
    int inp[] = {2, 3, 5, 4, 5, 3, 4}, len = 0, i =0, res = 0;
    
    len = sizeof(inp)/sizeof(inp[0]);
    for(i = 0; i < len; i++)
    {
        res ^= inp[i];
    }
    
    printf("Result is %d", res);
    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
