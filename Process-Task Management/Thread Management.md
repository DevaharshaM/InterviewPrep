# Thread Management

[Thread](https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Process-Task%20Management/Understanding%20important%20terms.md) Management refers to how the operating system handles the creation, scheduling, synchronization, and termination of threads within a process. Efficient thread management enables concurrent execution, better CPU utilization, and improved application performance. 

---

## Thread Lifecycle

The diagram below illustrates a typical thread lifecycle:

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Process-Task%20Management/lifecycle.png">
 <figcaption>Figure 1: Process lifecycle</figcaption>
</figure>

---

## Thread Creation

POSIX Threads (pthreads) – C

```c
#include <pthread.h>
#include <stdio.h>

void* printMessage(void* arg) 
{
    printf("Hello from thread!\n");
    return NULL;
}

int main() 
{
    pthread_t tid;
    pthread_create(&tid, NULL, printMessage, NULL);
    pthread_join(tid, NULL);  // Wait for thread to finish
    return 0;
}
```

---

## Types of Threading Models

| Model	                     | Description                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------|
| User-Level Threads (ULT)	 | Managed by a user-level library (e.g., pthreads). Faster but can't benefit from multiprocessor systems. |
| Kernel-Level Threads (KLT) |	Managed by the OS. Each thread is scheduled individually.                                              |
| Hybrid Threads	         | Combines benefits of both ULT and KLT (e.g., Linux NPTL, Windows threads).                              |

---

## Benefits of Threading

- Improved application responsiveness
- Better resource utilization on multicore systems
- Easier structuring of concurrent tasks