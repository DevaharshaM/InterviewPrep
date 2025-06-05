# Context Switching

**Context switching** is the process of storing and restoring the state (or context) of a CPU so that execution can be resumed from the same point at a later time. It enables an operating system to multitask by switching between different processes or threads.

---

## Why is Context Switching Needed?

- To allow **multitasking** (multiple processes appear to run simultaneously)
- To switch between **user processes** and **kernel tasks**
- To share CPU time among **multiple threads** or **processes**
- To implement **preemptive scheduling**

## What Gets Saved During a Context Switch?

When a context switch occurs, the following data is typically saved and restored:

- Program Counter (PC)
- CPU Registers
- Stack Pointer (SP)
- Process State (e.g., Ready, Waiting)
- Memory Management Info (e.g., page tables)

---

## PCB and TCB

### Process Control Block (PCB)

Used when switching **between processes**. It stores:

- Process ID (PID)
- Register contents
- Memory maps
- File descriptors
- CPU scheduling info

### Thread Control Block (TCB)
Used for switching **between threads**. It stores:

- Thread ID (TID)
- Thread state (Running, Waiting, etc.)
- Program counter
- Stack pointer
- Registers (specific to the thread)
- Scheduling priority

> In many systems, **TCBs are embedded inside or linked to PCBs**, especially when using kernel-level threads.

---

## Thread vs Process Switching

| Feature               | Process Switching          | Thread Switching          |
|------------------------|-----------------------------|----------------------------|
| Memory Space           | Different (full switch)     | Shared (within same process) |
| Speed/Overhead         | Higher                      | Lower                      |
| Requires MMU Context Switch | ✅                      | ❌ (if within same process) |

---

## Performance Impact

- **Context switching is not free** — it introduces CPU overhead.
- Involves:
  - Saving/restoring registers
  - Flushing and reloading CPU cache
  - Possible memory management reloads (page tables)
- Too many switches lead to **thrashing** or reduced throughput.

---

## Example

Suppose Process A is running and its time slice expires. The OS will:
1. Save A’s CPU state into its PCB.
2. Select Process B from the ready queue.
3. Load B’s state from its PCB into the CPU.
4. Resume execution from where B left off.
