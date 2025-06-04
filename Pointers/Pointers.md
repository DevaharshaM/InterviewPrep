# Pointers in C 

Pointers are one of the most important and powerful features in C. They allow direct memory access and manipulation, essential for systems-level programming, embedded systems, and writing efficient code.

---

## What Is a Pointer?

A pointer is a variable that stores the **address of another variable**.

### Example:

```c
#include <stdio.h>

int main()
{
    int a = 10;
    int *p = &a;

    *p += 5;

    printf("%d\n", a);  
    return 0;
}
```

### Explanation:

- p holds the address of a
- *p accesses the value at that address (i.e., a)
- *p += 5 modifies a to become 15

---

## What Is a Double Pointer?

A double pointer is a pointer to another pointer. It's often used in:
- Dynamic memory (e.g., 2D arrays)
- Function arguments where a pointer needs to be updated
- Advanced data structures

### Example:

```c
#include <stdio.h>

int main()
{
    int a = 10;
    int *p = &a;
    int **pp = &p;

    **pp += 5;
    *p += 2;

    printf("%d\n", a); 
    return 0;
}
```

### Explanation:
- a = 10: An integer initialized to 10.
- p = &a: p is a pointer holding the address of a.
- pp = &p: pp is a double pointer holding the address of p.
- **pp += 5:<br>
   o *pp gives us p, which points to a<br>
   o **pp accesses a → a = a + 5 = 15
- *p += 2:
   o *p accesses a again → a = a + 2 = 17
- Final output: 17

---

## What is a Function Pointer?

A function pointer stores the address of a function — it lets you call functions dynamically or pass them as arguments.

### Example:

```c
#include <stdio.h>

void greet()
{
    printf("Hello!\n");
}

int main()
{
    void (*fptr)() = greet;

    fptr();  // Calls greet()

    return 0;
}
```

--- 

## Advantages of Using Pointers

Pointers are essential in C programming because they enable:
- Dynamic Memory Allocation: Using functions like malloc(), calloc(), etc.
- Efficient Function Arguments: Passing large data structures by reference instead of by value.
- Direct Memory Access: Useful in systems programming and embedded systems.
- Data Structures: Crucial for implementing linked lists, trees, graphs, etc.
- Function Callbacks: Via function pointers, enabling dynamic behavior.

---

## Common Types of Pointers in C

1. Null Pointer (NULL)

A pointer that points to nothing.

### Example:

```c
int *p = NULL;
```

2. Void Pointer (void *)
   
A generic pointer that can point to any data type.

### Example:

```c
void *ptr;
int x = 5;
ptr = &x;
```

3. Dangling Pointer

A pointer that refers to memory that has been freed or is out of scope.

### Example:

```c
int *p;
{
    int x = 10;
    p = &x;
}
// p is now dangling
```

4. Wild Pointer
   
A pointer declared but not initialized.

### Example:

```c
int *p;  // uninitialized
*p = 10; // ⚠️ undefined behavior
```

5. Constant Pointers

- Pointer to Constant Value:

```c
const int *p = &a; // You can change p, but not *p.
```

- Constant Pointer:

```c
int *const p = &a; // You can change *p, but not p itself.
```

- Constant Pointer to Constant Value:

```c
const int *const p = &a; // Neither p nor *p can be changed.
```

---

# Bonus: Arrays of Function Pointers

Arrays of function pointers are useful when you want to call one of several functions based on a condition, like a function dispatch table.

### Example:

```c
#include <stdio.h>

void add()    
{
   printf("Add\n");
}
void subtract()
{
  printf("Subtract\n");
}
void multiply()
{
  printf("Multiply\n");
}

int main()
{
    void (*operations[3])() = {add, subtract, multiply};

    operations[0]();  // Calls add
    operations[2]();  // Calls multiply

    return 0;
}
```
