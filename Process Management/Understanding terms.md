# Understanding Programs, Processes, Tasks, and Threads

---

## What is a Program?

A program is a static file containing instructions written in a programming language (e.g., a .exe, .out, or .py file). It resides on disk and does nothing until executed.

## What is a Process?

A process is a program in execution. It includes:

- Executable code
- Current state (e.g., registers, program counter)
- Stack, heap, and memory space
- Open file descriptors and system resources

Each process is independent and managed by the OS.

## What is a Task?

The term task is often used interchangeably with process or thread, depending on the context:

- In some systems (e.g., Linux), it's a synonym for a process.
- In real-time or embedded systems, a task may refer to a lightweight schedulable unit, often equivalent to a thread.

## What is a Thread?

A thread is the smallest unit of execution within a process. Multiple threads within the same process:

- Share the same address space (heap, globals)
- Have their own registers, stack, and program counter
- Can run concurrently (parallelism or interleaving)

Threads are lighter and more efficient to switch between than full processes.

---

## Multithreading vs Multiprocessing

| Feature	      | Multithreading	                      | Multiprocessing           |
|-----------------|---------------------------------------|---------------------------|
| Memory Space	  | Shared among threads	              | Separate for each process |
| Overhead	      | Low	                                  | High                      |
| Communication	  | Easy (shared memory)	              | Complex (IPC needed)      |
| Fault Isolation |	Low (one thread crash can affect all) |	High (isolated processes) |

---

# Summary

| Term	  | Stored Where |	When Active	| Shares Memory?       | Lightweight? |
|---------|--------------|--------------|----------------------|--------------|
| Program |	Disk	     | Not yet	    | N/A	               | N/A          |
| Process |	RAM	         | Yes	        | No	               | No           | 
| Thread  |	RAM	         | Yes	        | Yes (within process) | Yes          |
| Task	  | Varies	     | Yes	        | Depends              | Depends      |