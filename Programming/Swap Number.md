# Swap two numbers

---

## Method 1: Using a Temporary Variable

```c
void swapNumber(int *num1, int *num2)
{
    int temp = *num1;
    *num1 = *num2;
    *num2 = temp;
}
```

**Time Complexity**: `O(1)`<br>
**Space Complexity**: `O(1)`

## Method 2: Using Arithmetic Operations

```c
void swapNumber(int *num1, int *num2)
{
    *num1 = *num1 + *num2;
    *num2 = *num1 - *num2;
    *num1 = *num1 - *num2;
}
```

**Time Complexity**: `O(1)`<br>
**Space Complexity**: `O(1)`
> Not safe if values are large — risk of integer overflow.

## Method 3: Without Temporary Variable (XOR Bitwise)

```c
void swapNumber(int *num1, int *num2)
{
    *num1 = *num1 ^ *num2;
    *num2 = *num1 ^ *num2;
    *num1 = *num1 ^ *num2;
}
```

**Time Complexity**: `O(1)`<br>
**Space Complexity**: `O(1)`
> Safe from overflow, but only works reliably on integer types.

---

# main() function

```c
/* include required header files */
#include <stdio.h>

/* function declaration to swap numbers */
void swap(int *num1, int *num2);

/* main function */
int main()
{
    int a = 10, b = 20;
    printf("Before Swapping - a: %d, b: %d\n", a, b);

    /* function call to swap numbers */
    swapNumber(&a, &b);

    printf("After Swapping  - a: %d, b: %d\n", a, b);
    return 0;
}
```
