# Scheduling Algorithms

In a multitasking operating system, **CPU scheduling** determines the order in which processes are allowed to use the CPU. The goal is to improve system performance by maximizing CPU usage, minimizing wait times, and ensuring fair access to resources.

The **scheduler** makes these decisions based on a defined algorithm and manages the **ready queue** of processes.

---

## Objectives of Scheduling

- Maximize CPU utilization
- Minimize waiting and turnaround time
- Improve responsiveness for interactive systems
- Ensure fairness and avoid starvation

---

## Common Scheduling Algorithms

| Algorithm | Description | Preemptive? |
|-----------|-------------|-------------|
| **FCFS** (First-Come, First-Served) | Processes executed in arrival order. | ❌ |
| **SJF** (Shortest Job First) | Picks process with the smallest burst time. | ❌ (or ✅ as SRTF) |
| **Round Robin (RR)** | Time-sharing; each process gets a fixed time slice (quantum). | ✅ |
| **Priority Scheduling** | Executes process with the highest priority. | ✅ / ❌ |
| **Multilevel Queue** | Multiple queues based on process type or priority. | ✅ |
| **Multilevel Feedback Queue (MLFQ)** | Allows processes to move between queues based on behavior. | ✅ |

### Example: FCFS

### Input:
| Process | Arrival Time | Burst Time |
|---------|--------------|------------|
| P1      | 0            | 4          |
| P2      | 1            | 3          |
| P3      | 2            | 1          |

### Gantt Chart:

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Process-Task%20Management/gantt.png">
 <figcaption>Figure 1: Gantt Chart</figcaption>
</figure>

### Average Waiting Time:
- P1: 0  
- P2: 3  
- P3: 6  
**Average = (0 + 3 + 6) / 3 = 3**

---

## Preemptive vs Non-Preemptive

| Feature       | Preemptive                    | Non-Preemptive                 |
|---------------|-------------------------------|--------------------------------|
| Can interrupt | ✅                             | ❌                              |
| Examples      | Round Robin, SRTF             | FCFS, SJF                      |
| Use Case      | Interactive/real-time systems | Simple batch processing        |

---

# Bonus: Scheduling in Real Devices

## Android Devices – **Completely Fair Scheduler (CFS)**

Android uses the **CFS**, inherited from the Linux kernel. It is a **preemptive, priority-based** scheduler optimized for responsiveness and fairness.

### How CFS Works:
- Maintains a **red-black tree** of runnable processes, sorted by **virtual runtime** (time process has had the CPU).
- Selects the **leftmost (least used) process** for the next execution.
- Gives each process a **fair share** of CPU time based on weight (priority).
- Supports **nice values**, **cgroups**, and **real-time scheduling policies** (`SCHED_FIFO`, `SCHED_RR`).

### Key Features:
- Fair distribution of CPU time
- Good for multi-core systems
- Respects process priority (nice values)
- Energy-aware (especially in Android)

## Linux Desktops & Servers – **CFS**

The **default scheduler** in modern Linux systems (since kernel 2.6.23).

### Highlights:
- No fixed time quantum; scheduling depends on time already spent on the CPU
- More **smooth and responsive** than Round Robin or MLFQ
- Good for **desktop workloads, servers, and real-time systems**

## Windows 10/11 – **Hybrid Priority-Based Scheduler**

- Based on **priority classes** and **dynamic boosting**
- Combines **preemptive scheduling** and **MLFQ concepts**
- Prioritizes foreground/interacting tasks
- Background tasks get lower priority unless manually adjusted

## Apple Devices – macOS / iOS

Apple’s operating systems use a scheduler derived from **XNU**, which combines **BSD** (Unix-like) and **Mach** microkernel features.

### Apple’s Scheduling Approach:
- Preemptive and priority-based
- Supports **thread groups** and **QoS (Quality of Service) classes**:
  - `UserInteractive`, `UserInitiated`, `Utility`, `Background`
- Uses **work queues** and **Grand Central Dispatch (GCD)** to abstract thread scheduling
- Prioritizes **responsiveness and battery life** on mobile devices

## Summary:

| Platform | Scheduler Type | Notes |
|----------|----------------|-------|
| **Android** | Linux CFS + cgroups | Energy-aware and interactive tuning |
| **Linux** | CFS | Red-black tree, fair, responsive |
| **Windows** | Hybrid MLFQ + priority | Boosts interactive performance |
| **Apple** | XNU hybrid | Uses QoS classes and GCD for concurrency |
