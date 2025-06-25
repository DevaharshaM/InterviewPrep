# Check if a string is a Palindrome

A **palindrome** is a word, phrase, or sequence that reads the same backward as forward.

Examples:
- "madam" → Palindrome  
- "racecar" → Palindrome  
- "hello" → Not a palindrome

---
## Code

```c
/* include required header files */
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

/* function definition for checking palindrome */
bool checkPalindrome(char *str)
{
    int len = 0, i = 0, j = 0;
    bool flagPalindrome = true;
    
    len = strlen(str);
    i = 0, j = len-1;
    
    while(i < j)
    {
       if(str[i] != str[j])
       {
           flagPalindrome = false;
           break;
       }
       else
       {
           /* Do Nothing */
       }
       
       i++;
       j--;
    }
    
    return flagPalindrome;
}

/* main function */
int main()
{
    char a[] = "racecar";
    bool resFlag = false;
    
    /* function call for checking palindrome */
    resFlag = checkPalindrome(a);
    
    if(resFlag == 1)
    {
        printf("Palindrome");
    }
    else
    {
        printf("Not a Palindrome");
    }
    
    return 0;
}
```

## [Time & Space Complexity](https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Programming/Time%20%26%20Space%20Complexity%20in%20C.md)

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
