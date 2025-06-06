# Paging and Segmentation

Modern operating systems use **paging** and **segmentation** to manage memory efficiently. These techniques allow the OS to:
- Isolate process memory
- Eliminate fragmentation
- Translate virtual addresses to physical addresses

---

## Page Table

The **page table** is a critical data structure that maps **virtual pages** to **physical frames**.

Each process has its own page table. The **Memory Management Unit (MMU)** uses it to translate addresses during execution.

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Memory%20Management/pagetable.png">
 <figcaption>Figure 1: Page table</figcaption>
</figure>

<br><br>In this example:
- **Page Size = Frame Size = 2KB**
- A process with **4KB** of virtual memory has **2 pages**
- RAM has **16KB**, giving **8 physical frames**

The **virtual address** is split into:
- **Page Number**: identifies the page within the process
- **Offset**: byte position within that page

The **page table** maps virtual pages to physical frames, enabling address translation.

---

## Paging

**Paging** divides:
- Virtual memory into fixed-size **pages**
- Physical memory into fixed-size **frames**

### Benefits
- Eliminates **external fragmentation**
- Enables non-contiguous allocation
- Simple to implement

### Drawback
- Can suffer from **internal fragmentation** (unused space within a frame)

---

## Key Terms

| Term           | Description |
|----------------|-------------|
| **Page Fault** | Requested page is not in RAM; triggers loading from disk |
| **Page Hit**   | Requested page is found in physical memory |
| **TLB Miss**   | Entry not found in Translation Lookaside Buffer; requires page table lookup |
| **Page Replacement** | Happens when memory is full and a new page must be loaded |

---

## Page Replacement Algorithms

When a **page fault** occurs and there are **no free frames**, the OS must choose a victim page to evict.

| Algorithm | Description |
|-----------|-------------|
| **FIFO**  | Evicts the oldest loaded page |
| **LRU**   | Evicts the least recently used page |
| **Optimal** | Evicts the page that won’t be used for the longest time (requires future knowledge) |
| **Clock** | Approximates LRU with less overhead using a circular buffer and a use-bit |

> In real-world systems, **Clock** or **approximated LRU** is often used for performance reasons.

---

## Segmentation

**Segmentation** divides a program's memory into **logical units**:
- Code
- Data
- Stack
- Heap

Each segment is:
- **Variable-sized**
- Associated with a **segment number**, **base address**, and **limit**

### Drawback
- Suffers from **external fragmentation**
- Can be reduced using **segmentation with paging**

---

## Fragmentation

Fragmentation refers to the inefficient use of memory that prevents full utilization, even if enough total space exists.

### 1. Internal Fragmentation

Occurs in **paging** when:
- A process does not use the entire space allocated in a page frame
- The **unused space** within the frame is wasted

> Example: Page size = 2KB, process needs 3KB → 2 pages used → 1KB wasted

### 2. External Fragmentation

Occurs in **segmentation** when:
- Memory is divided into **variable-sized segments**
- Free memory is available but **not in a contiguous block**, preventing allocation

> Example: You have 3 free blocks of 1KB, 2KB, and 3KB, but can't allocate a 4KB segment — even though total free space = 6KB

---

## Paging vs Segmentation

| Feature           | Paging                        | Segmentation                     |
|-------------------|-------------------------------|----------------------------------|
| Division Unit     | Fixed-size pages              | Variable-size segments           |
| Fragmentation     | Internal                      | External                         |
| Addressing        | Page number + offset          | Segment number + offset          |
| Use Case          | Efficient memory management   | Logical program structuring      |
