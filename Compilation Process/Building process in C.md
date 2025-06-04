# Compiler Toolchain

The C build process (`.c` file to `.hex` or `.elf` file) involves several stages, handled by the **compiler toolchain**.

---

## Stages in the Compilation Process

Let’s break down the process from source code to executable binary:

---

### 1. **Preprocessing (`.c` → expanded source)**

Handled by: **Preprocessor**

```bash
gcc -E main.c -o main.i
```

- Expands #include files
- Replaces macros (#define)
- Handles conditional compilation (#ifdef, #ifndef)

> Output: a .i file (intermediate expanded source)

### 2. **Compilation (`.i` → Assembly)**

Handled by: **Compiler proper**

```bash
gcc -S main.i -o main.s
```

- Converts the preprocessed code into assembly language
- Architecture-specific (e.g., x86, ARM)

> Output: .s file (human-readable assembly code)

### 4. **Assembly (`.s` → Object Code)**

Handled by: **Assembler**

```bash
gcc -c main.s -o main.o
```

- Translates assembly to machine code
- Produces relocatable object files

> Output: .o file (binary, not yet executable)

### **Linking (`.o` → Executable or Binary Image)**

Handled by: **Linker**

```bash
gcc main.o -o main.elf
```

- Combines multiple .o files and libraries
- Resolves function calls, symbols, and memory layout
- Outputs a complete binary (e.g., .elf, .exe, .bin)

> Output: .elf file (Executable and Linkable Format)

### 5. **Converting `.elf` to `.hex` for microcontrollers*

Handled by: **Objcopy (GNU binutils)**

```bash
arm-none-eabi-objcopy -O ihex main.elf main.hex
```

- Converts to Intel HEX format, used for microcontroller flashing

---

## Summary

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/cProgramming/Compilation%20Process/toolchain.png">
 <figcaption>Figure 1: Compiler Toolchain</figcaption>
</figure>
