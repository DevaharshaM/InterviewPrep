# Disk Scheduling Algorithms

---

To understand disk scheduling, it's helpful to first understand how a hard disk is physically structured.

<figure>
<img src = "https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/File%20System%20Management/harddisk.png">
<figcaption>Figure 1: Hard Disk Architecture</figcaption>
</figure>

### Key Components:

- **Platters**: Circular magnetic disks where data is stored.
- **Tracks**: Concentric circles on each platter surface.
- **Sectors**: Smallest addressable storage unit within a track.
- **Spindle**: Rotates the platters at a fixed RPM (e.g., 5400 or 7200 RPM).
- **Read/Write Head**: Reads or writes data to a specific sector.
- **Arm**: Moves the R/W head across tracks.

### Head Movement:

- The **arm** moves the **read/write head** to the correct **track** (seek operation).
- The **spindle** rotates the **platter** to bring the correct **sector** under the head (rotational latency).

> Together, seek time and rotational latency define the time to access data on disk.

---

## Introduction

**Disk scheduling algorithms** determine the order in which pending I/O requests are serviced by the disk controller.  
Their goal is to:
- Minimize **seek time**
- Improve **throughput**
- Ensure **fairness** among requests

---

## Key Disk Access Times

| Term               | Description |
|--------------------|-------------|
| **Seek Time**      | Time to move the disk arm to the correct track |
| **Rotational Latency** | Time for the desired sector to rotate under the head |
| **Transfer Time**  | Time to transfer data once the sector is aligned |

> Disk scheduling focuses mostly on reducing **seek time**, which is the most time-consuming part.

---

## Common Disk Scheduling Algorithms

---

### 1. **FCFS (First-Come, First-Served)**

- Serve requests in the order they arrive.
- ✅ Fair  
- ❌ May result in long total head movement

---

### 2. **SSTF (Shortest Seek Time First)**

- Picks the request closest to current head position.
- ✅ Optimizes seek time  
- ❌ Can starve far-away requests

---

### 3. **SCAN (Elevator Algorithm)**

- Head moves in one direction servicing requests until the end, then reverses.
- ✅ Prevents starvation  
- ❌ Delays for requests in the reverse direction

---

### 4. **C-SCAN (Circular SCAN)**

- Head moves in one direction only.
- After reaching end, jumps back to start and resumes.
- ✅ More uniform wait times than SCAN

---

### 5. **LOOK**

- A smarter version of SCAN.
- Head only goes as far as the last request before reversing — doesn't go to end of disk unless needed.

---

### 6. **C-LOOK**

- Like C-SCAN, but only jumps from last request back to first (not full disk end).

---

## Comparison

| Algorithm | Avg Seek Time | Starvation | Directional Scan |
|-----------|----------------|------------|------------------|
| FCFS      | Poor            | No         | No               |
| SSTF      | Better          | Yes        | No               |
| SCAN      | Good            | No         | Yes              |
| C-SCAN    | Fair            | No         | One-way          |
| LOOK      | Better than SCAN| No         | Yes              |
| C-LOOK    | Best fairness   | No         | One-way          |

---

## Example: Seek Time Calculation

**Head Start Position: 53**  
**Request Queue:** [98, 183, 37, 122, 14, 124, 65, 67]

### FCFS Order:
53 → 98 → 183 → 37 → 122 → 14 → 124 → 65 → 67  
➡️ Total head movement = large

### SSTF Order:
Serve requests closest to current head → much shorter total head movement  
(e.g., 53 → 65 → 67 → 37 → 14 → 98 → 122 → 124 → 183)

---

# Summary

- **Disk scheduling improves efficiency** by minimizing disk arm movements.
- **SSTF** is efficient but unfair.
- **SCAN, LOOK, C-SCAN, C-LOOK** offer better fairness and are more commonly used.
- Real systems may combine algorithms depending on workload type.
