# Count Number of 1s and 0s in Binary Representation

---

This program counts the number of **set bits (1s)** and **unset bits (0s)** in the binary representation of a given non-negative integer.

📌 Example:  
Input: 15  
Binary: 00000000 00000000 00000000 00001111 (for 32-bit int)  
Output: 4 ones, 28 zeroes

---

## Code
```c
/* include required header files */
#include <stdio.h>

/* main function */
int main()
{
    int num = 15, temp = num, i = 0, cntOnes = 0, cntZeroes = 0;
    
    while(temp)
    {
        cntOnes++;
        temp = temp & (temp-1);
    }
    cntZeroes = (sizeof(num) * 8) - cntOnes;
    
    printf("%d's binary has %d 1's and %d 0's", num, cntOnes, cntZeroes);
    
    return 0;
}
```
