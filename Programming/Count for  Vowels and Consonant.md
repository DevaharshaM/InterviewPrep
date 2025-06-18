# Count Vowels and Consonants in a String

---

> Assumes the input contains only **lowercase letters**

```c
/* include required header files */
#include <stdio.h>

/* main function */
int main()
{
    char a[] = "happy coding";
    int cntVowel = 0, cntConsonant = 0, i = 0;
    
    for(i = 0; a[i] != '\0'; i++)
    {
        /* check the character is a valid alphabet */
        if((a[i] >= 'a') && (a[i] <= 'z'))
        {
            /* check for vowels */
            if((a[i] == 'a') || (a[i] == 'e') || (a[i] == 'i') || (a[i] == 'o') || (a[i] == 'u'))
            {
                /* count vowels */
                cntVowel++;
            }
            else
            {
                /* count consonants */
                cntConsonant++;
            }
        }
        else
        {
            /* Do Nothing */
        }
    }
    printf("Vowels: %d, Consonants: %d", cntVowel, cntConsonant);

    return 0;
}
```

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
