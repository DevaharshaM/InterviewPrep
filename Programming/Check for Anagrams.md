# Check If Two Strings Are Anagrams

An **anagram** is a word or phrase formed by rearranging the letters of another, using all original letters exactly once.

Example: "listen" and "silent" are anagrams.

---
> assuming both strings contain only **lowercase English letters** (`'a'` to `'z'`).

```c
/* include required header files */
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

/* function definition for checking anagrams */
bool checkAnagram(char *str1, char *str2)
{
    bool flagAnagram = true;
    int alphabetArray[26] = {0,}, len1 = 0, len2 = 0, i = 0;
    
    len1 = strlen(str1);
    len2 = strlen(str2);
    
    if(len1 != len2)
    {
        flagAnagram = false;
    }
    else
    {
        for(i = 0; i < len1; i++)
        {
            alphabetArray[str1[i]-'a']++;
            alphabetArray[str2[i]-'a']--;
        }
        
        for(i = 0; i < 26; i++)
        {
            if(alphabetArray[i])
            {
                flagAnagram = false;
                break;
            }
            else
            {
                /* Do Nothing */
            }
        }
    }
    
    return flagAnagram;
}

/* main function */
int main()
{
    char a[] = "listen", b[] = "silent";
    bool resFlag = false;
    
    /* function call for checking anagrams */
    resFlag = checkAnagram(a,b);
    
    if(resFlag == 1)
    {
        printf("Given strings are Anagrams");
    }
    else
    {
        printf("Given strings are not Anagrams");
    }
    return 0;
}
```

**Time Complexity**: `O(n)`<br>
**Space Complexity**: `O(1)`
