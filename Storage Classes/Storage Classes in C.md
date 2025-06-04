# Storage Classes in C

In C, **storage classes** define the *scope*, *visibility*, *lifetime*, and *linkage* of variables. They tell the compiler how and where to store the variables and how long they should persist.

C provides four primary storage classes:

- `auto`
- `register`
- `static`
- `extern`

---

## auto

The auto storage class is the default for local variables declared inside functions or blocks.

```c
void func() {
    auto int x = 10; // same as: int x = 10;
}
```

o Scope: Local to the block<br>
o Lifetime: Created on entry, destroyed on exit<br>

## register

The register storage class is a request to store the variable in a CPU register instead of RAM, for faster access.

```c
void func() {
    register int counter = 0;
}
```

o Scope: Local<br>
o Lifetime: Same as `auto`

## static

The static storage class modifies the lifetime and linkage of variables and functions.

```c
void func() {
    static int counter = 0;
    counter++;
    printf("%d\n", counter);
}
```

o Scope: <br>
        - Inside function: local scope<br>
        - Outside function: file scope<br>
o Lifetime: Entire program

## extern

The extern storage class is used to declare a variable or function that is defined in another file or later in the same file.

```c
// file1.c
int shared = 10;

// file2.c
extern int shared;
```

o Scope: Global across files<br>
o Lifetime: Entire program

---

## Summary

| Storage Class | Scope         | Lifetime         | Linkage     | Visibility            | Default Value   |
|---------------|---------------|------------------|-------------|------------------------|------------------|
| `auto`        | Block         | Block duration   | None        | Within the block       | Garbage          |
| `register`    | Block         | Block duration   | None        | Within the block       | Garbage          |
| `static`      | Block/File    | Entire program   | Internal    | Within block or file   | Zero             |
| `extern`      | Global        | Entire program   | External    | Visible across files   | Depends on def   |
