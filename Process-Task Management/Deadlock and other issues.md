# ⛔ Deadlocks, Starvation, and Priority Inversion

In concurrent systems, improper synchronization can lead to critical issues like **deadlocks**, **starvation**, and **priority inversion**. These problems disrupt the fair execution of processes and can severely impact system responsiveness or even cause hangs.

---

## What is a Deadlock?

A **deadlock** occurs when a set of processes are blocked, each waiting for a resource held by another process in the set — and none of them can proceed.

### Example:

- Process A holds Resource 1, needs Resource 2
- Process B holds Resource 2, needs Resource 1
- Both wait indefinitely: **deadlock**

## Four Necessary Conditions for Deadlock

| Condition         | Description |
|-------------------|-------------|
| **Mutual Exclusion**   | At least one resource must be non-shareable |
| **Hold and Wait**      | A process holds one resource while waiting for another |
| **No Preemption**      | A resource can't be forcibly taken from a process |
| **Circular Wait**      | A circular chain of processes exists, each waiting for a resource held by the next |

> All four must hold simultaneously for a deadlock to occur.

## Handling Deadlocks

### 1. **Deadlock Prevention**

Break one of the four conditions (e.g., don’t allow hold-and-wait).

### 2. **Deadlock Avoidance**

Use strategies like **Banker’s Algorithm** to analyze safe states before allocating resources.

#### Banker's Algorithm

The **Banker’s Algorithm** is a **deadlock avoidance** strategy developed by Edsger Dijkstra. It ensures the system always stays in a **safe state** by simulating the allocation of resources before actually granting them.

##### How It Works

When a process requests resources:
1. Simulate granting the request.
2. Check if the system remains in a **safe state**.
3. If safe → grant the request.  
   If unsafe → deny or delay it.

✅ A **safe state** means that all processes can still finish eventually, even if they request their **maximum** resources.


##### Example

| Process | Max Need | Allocated | Remaining |
|---------|----------|-----------|-----------|
| P1      | 7        | 5         | 2         |
| P2      | 3        | 2         | 1         |
| P3      | 9        | 4         | 5         |

**Available**: 3 units  
Process **P2 requests 1** more unit.

##### Simulation:
- Grant request → Available = 2
- P2 finishes → releases 3 → Available = 5
- P3 can now finish
- Then P1

✅ System is safe → grant request.

### 3. **Deadlock Detection & Recovery**

Let deadlocks occur and detect them using wait-for graphs, then:
- Kill one or more processes
- Preempt resources

---

## Starvation

**Starvation** happens when a process waits **indefinitely** to access a resource because others keep getting scheduled before it.

> Example: A low-priority process never runs if higher-priority ones always dominate the CPU.

### Prevention:

- **Aging**: Gradually increase a process’s priority the longer it waits.

---

## Priority Inversion

**Priority Inversion** occurs when a **low-priority process holds a resource** needed by a **high-priority process**, blocking the high-priority one.

### Example:
1. Low-priority thread locks a mutex
2. High-priority thread needs that mutex → gets blocked
3. Medium-priority threads run (OS keeps switching to them)
4. Low-priority thread can't finish → **inversion**

### Solution: Priority Inheritance

- Temporarily **boost the priority** of the low-priority thread holding the resource
- Let it complete, release the lock
- Then return to normal priorities

---

## Summary

| Issue              | Cause                             | Prevention / Solution          |
|--------------------|-----------------------------------|--------------------------------|
| **Deadlock**        | Circular waiting, no preemption   | Prevention, Avoidance, Detection |
| **Starvation**      | Priority/resource bias            | Aging or fair scheduling       |
| **Priority Inversion** | High-priority thread blocked by low | Priority Inheritance          |