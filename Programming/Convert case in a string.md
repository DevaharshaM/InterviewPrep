# Convert Uppercase to Lowercase in a string

---

> Assumes the input contains only alphabetic characters

```c
/* include required header files */
#include <stdio.h>

/* function definition to convert upper case to lower case */
void convertUtoL(char *str)
{
    int i = 0;
    
    for(i = 0; str[i] != '\0'; i++)
    {
        if((str[i] >= 'A') && (str[i] <= 'Z'))
        {
            str[i] = str[i] + 32;
        }
    }
}

/* main function */
int main()
{
    char a[] = "HeLLo";
    
    /* function call to convert upper case to lower case */
    convertUtoL(a);
    
    printf("%s", a);
    return 0;
}
```

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
