# Reverse a String

---
## Code
```c
/* include required header files */
#include <stdio.h>
#include <string.h>

/* function definition for swapping character */
void swap(char *x, char *y)
{
    char temp;
    temp = *x;
    *x = *y;
    *y = temp;
}

/* function definition for reversing string */
void reverse(char *str)
{
    int len = 0, i = 0, j = 0;
    
    len = strlen(str);
    i = 0, j = len-1;
    
    while(i < j)
    {
        swap(&str[i], &str[j]);
        i++;
        j--;
    }
}

/* main function */
int main()
{
    char a[] = "hello";
    
    /* function call for reversing string */
    reverse(a);
    
    printf("%s", a);
    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
