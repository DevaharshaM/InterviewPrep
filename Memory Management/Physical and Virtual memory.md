# Physical & Virtual memory

Memory management is a core responsibility of the operating system. It ensures efficient use of physical memory and enables processes to run in isolation using **virtual memory**.

Modern operating systems **abstract physical memory** through virtual memory, allowing:
- Process isolation
- Protection
- Efficient memory allocation
- Larger-than-physical memory usage

---

## Physical vs Virtual Memory

| Memory Type      | Description |
|------------------|-------------|
| **Physical Memory** | Actual RAM installed on the system |
| **Virtual Memory**  | Logical abstraction of memory presented to each process; mapped to physical memory by the OS and MMU (Memory Management Unit) |

> Each process believes it has its own private, continuous memory — but the OS maps it behind the scenes.

---

## Virtual Addresses

A **virtual address** is the memory address a process uses. It must be **translated** into a physical address before accessing real RAM.

- Virtual addresses are **process-specific**
- Physical addresses are **system-wide**

---

## Address Translation

To access memory, the OS uses a **mapping system** (usually paging) to convert **virtual addresses → physical addresses**.

### Basic Flow:
1. CPU generates a **virtual address**
2. MMU uses a **page table** to look up the corresponding **physical frame**
3. If page is not in memory → **page fault** occurs

---

### Components in Translation:

- **Page Table**: Maps virtual pages to physical frames
- **MMU (Memory Management Unit)**: Hardware that performs the translation
- **TLB (Translation Lookaside Buffer)**: A small, fast cache that stores recent virtual-to-physical translations

> TLB reduces access time by avoiding page table lookups for frequently accessed addresses.