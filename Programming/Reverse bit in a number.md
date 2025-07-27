# Reverse Bits of a Number (Left to Right)

---

This program reverses the **binary representation** of a given integer using bitwise logic.

Example:
- Input: `13` → Binary: `01101`
- Output: `22` → Binary: `10110`

---
## Code

```c
/* include required header files */
#include <stdio.h>

/* function definition for finding bit length */
int bitWidth(int num)
{
    int count = 0;
    if (num == 0) return 1; // edge case
    while (num)
    {
        count++;
        num >>= 1;
    }
    return count;
}

/* function definition for reversing bits */
void reverseBit(int num, int len)
{
    int res = 0;
    for (int i = 0; i < len; i++)
    {
        int bit = (num >> i) & 1;
        res |= (bit << (len - 1 - i));
    }
    printf("Reversing bits results: %d", res);
}

/* main function */
int main()
{
    int inpNum = 13, bitLen = 0;

    /* function call for finding bit length */
    bitLen = bitWidth(inpNum);

    /* function call for reversing bit */
    reverseBit(inpNum, bitLen);

    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(n)` <br>
**Space Complexity**: `O(1)`
