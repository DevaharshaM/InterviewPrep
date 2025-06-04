# Memory Layout of a C Program

When a C program is compiled and run, its memory is divided into well-defined segments. The major memory segments are:

- Text (Code)
- Data
- BSS
- Heap
- Stack

<figure>
  <img src="https://github.com/DevaharshaM/InterviewPrep/blob/memory_layout/layout.png" alt="Memory Layout" style="max-width: 100%;">
  <figcaption>Figure: Memory layout of RAM</figcaption>
</figure>

---

## Text Segment

- Also known as the *code segment*.
- Stores compiled program instructions (machine code).
- Usually **read-only** to prevent accidental modification.
- May include constants like `const int a = 5;` depending on compiler/linker.

```c
int add(int a, int b) {
    return a + b;  // This lives in the text segment.
}
```

## Data Segment

- Stores initialized global and static variables.
- Values are known at compile time.

```c
int count = 10;         // Global, initialized → Data segment
static int flag = 1;    // Static, initialized → Data segment
```

## BSS Segment

- Stores uninitialized or zero-initialized global and static variables.
- Allocated at runtime and zeroed out.

```c
int total;              // Global, uninitialized → BSS segment
static float ratio;     // Static, uninitialized → BSS segment
```

## Heap Segment

- Used for dynamic memory allocation (`malloc, calloc, etc`).
- Grows upward at runtime as needed.
- Managed manually — requires `free()` to release memory.

```c
int *arr = malloc(10 * sizeof(int));  // Heap segment
```

## Stack Segment

- Stores function call frames, local variables, and return addresses.
- Grows downward (typically).
- Automatically managed — memory is reclaimed when the function returns.

```c
void func() {
    int local_var = 5;  // Stack segment
}
```
