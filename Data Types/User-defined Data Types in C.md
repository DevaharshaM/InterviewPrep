# User Defined Data Types

C provides **user-defined data types** that allow programmers to group, organize, and represent data in a meaningful way.  
The most commonly used user-defined data types are:

- `struct`
- `union`
- `enum`

---

## Structure (`struct`)

A struct allows you to group variables of different data types under a single name.

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
### Key Points:

- Each member has its own memory
- Total size = sum of sizes of all members plus padding
- Members can be accessed independently
  
### Use Cases:

- Representing real-world entities (like Student, Employee)
- Passing multiple related values to functions
- Building complex data structures (linked lists, trees, etc.)

## Union (union)

A union is similar to a struct, but all members share the same memory location.

### Example:

```c
union Data {
    int i;
    float f;
    char c;
};
```

### Key Points:

- Only one member is valid at a time
- Size of union = size of the largest member
- Writing to one member overwrites others

### Use Cases:

- Memory optimization
- Interpreting the same data in multiple ways
- Hardware register access in embedded systems

## Enumeration (enum)

An enum defines a set of named integer constants.

### Example:

```c
enum State {
    IDLE,
    BUSY,
    ERROR
};
```

### Key Points:

- Improves readability
- Avoids magic numbers
- Internally stored as integers

### Use Cases:

- State machines
- Mode selection
- Error codes

---

## Typedef

The typedef keyword creates an alias for an existing data type, improving code readability.

### Typedef with Structure:
```c
typedef struct {
    int x;
    int y;
} Point;

Point p1;
```
### Typedef with Enum:
```c
typedef enum {
    RED,
    GREEN,
    BLUE
} Color;

Color c = RED;
```
### Why Use typedef?

- Cleaner syntax
- Easier maintenance
- Common in APIs and embedded codebases

---

## Structure vs Union 

| Feature	        | struct	                      | union                               |
|-------------------|---------------------------------|-------------------------------------|
| Memory Allocation | Separate memory for each member     | Shared memory for all members   |
| Size	            | Sum of all member sizes (+ padding) | Size of largest member          |
| Access	        | All members accessible	          | Only one member valid at a time |
| Use Case	        | Data grouping	                      | Memory optimization             |

---

# BONUS: Structure Padding

Structure padding is the automatic insertion of unused bytes by the compiler to align data members for faster access.

## Example:

```c
struct Example {
    char a;
    int b;
};
```
### Explaination:

| Member  | Size    | Offset |
|---------|---------|--------|
| char a  |	1 byte  | 0      |
| padding |	3 bytes | 1–3    |
| int b   |	4 bytes | 4      |

👉 Total size = 8 bytes, not 5.

## Why Padding Happens:

- CPUs access aligned data faster
- Misaligned access can cause performance penalties or faults (especially in embedded systems)

## How to Reduce Padding:

- Reorder structure members from largest to smallest
- Use compiler-specific packing (with caution)

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
