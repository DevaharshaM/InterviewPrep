# Remove Duplicate Characters from a String

---
## Code
> Assumes the input string is null-terminated and contains only **lowercase English letters**.
```c
/* include required header files */
#include <stdio.h>
#include <string.h>

/* function definition to remove duplicates in a string */
void removeDuplicate(char *str)
{
    int temp[26] = {0,}, len = 0, i = 0, j = 0;
    
    len = strlen(str);
    for(i = 0; i < len; i++)
    {
        temp[str[i]-'a']++;
        if(temp[str[i]-'a'] == 2)
        {
            temp[str[i] - 'a']--;
        }
        else
        {
            str[j] = str[i];
            j++;
        }
    }
    str[j] = '\0';
}

/* main function */
int main()
{
    char a[] = "programming";
    
    /* function call to remove duplicates in a string */
    removeDuplicate(a);
    
    printf("%s", a);
    
    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
