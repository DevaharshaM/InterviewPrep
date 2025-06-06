# User Defined Data Types

C provides several ways to define custom data types that help organize code and make it more readable and scalable. The most common ones are `struct` and `enum`.

---

## What is a `struct`?

A `struct` (structure) groups variables of **different types** under a single name.

### Example:

```c
#include <stdio.h>

struct Person {
    char name[20];
    int age;
};

int main() {
    struct Person p1 = {"Alice", 25};
    printf("%s is %d years old.\n", p1.name, p1.age);
    return 0;
}
```

### Use Cases:

- Representing real-world entities (like Student, Employee)
- Passing multiple related values to functions
- Building complex data structures (linked lists, trees, etc.)

## What is an enum?

An enum (enumeration) defines a set of named integer constants.

### Example:

```c
#include <stdio.h>

enum Day { MON, TUE, WED, THU, FRI, SAT, SUN };

int main() {
    enum Day today = WED;

    if (today == WED)
        printf("Midweek!\n");

    return 0;
}
```

### Use Cases:

- Replacing magic numbers with named constants
- Representing states (e.g., IDLE, BUSY, ERROR)
- Using symbolic values in switch or if statements

---

## Typedef: Making User-Defined Types Easier to Use

The typedef keyword creates an alias for a data type, reducing verbosity and improving readability.

### Without typedef

```c
struct Point {
    int x, y;
};

struct Point p1;
```

### With typedef

```c
typedef struct {
    int x, y;
} Point;

Point p1;
```

### Typedef with enum

```c
typedef enum {
    RED, GREEN, BLUE
} Color;

Color c = GREEN;
```

### Benefits:

- Cleaner syntax
- Easier to use in large codebases
- Abstracts complexity in data structures and APIs

---

## struct vs enum 

| Feature	| struct	                      | enum                            |
|-----------|---------------------------------|---------------------------------|
| Purpose	| Group multiple variables	      | Name a set of related constants |
| Types	    | Can mix different data types	  | Only holds integers             |
| Memory	| Takes memory for each field	  | Just stores one integer         |
| Use Case	| Data models, complex structures | Modes, states, symbolic values  |
| Access	| Use dot/arrow for fields	      | Use by symbolic constant        |

---

# BONUS: Pointers to Structures

Using a pointer to a structure lets you:

- Pass large data efficiently to functions
- Modify data in-place
- Dynamically allocate structures

## Example:

```c
#include <stdio.h>

typedef struct {
    int x, y;
} Point;

int main() {
    Point pt = {3, 4};
    Point *p = &pt;

    printf("x: %d, y: %d\n", p->x, p->y);  // Use arrow operator
    return 0;
}
```

## Explanation:

- Point *p = &pt; → creates a pointer to the structure
- p->x accesses field x using the arrow (->) operator
- Equivalent to (*p).x