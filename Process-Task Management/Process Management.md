# Process Management

Process Management is a fundamental responsibility of the operating system. It involves handling the lifecycle and resources of processes to ensure efficient multitasking, stability, and fair use of the CPU and memory. 

---

## Process Lifecycle

A process transitions through several well-defined states during its execution. The diagram below illustrates a typical process lifecycle:

<figure>
 <img src = "https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Process-Task%20Management/lifecycle.png">
 <figcaption>Figure 1: Process lifecycle</figcaption>
</figure>

<br><br>Description of States:

- New: Process is being created.
- Ready: Process is ready to run, waiting for CPU allocation.
- Running: Process is being executed by the CPU.
- Waiting: Process is waiting for an event (e.g., I/O).
- Terminated: Process has completed execution.

---

## Process Creation

A process can create another process using system calls provided by the OS. This results in a parent-child relationship between processes.

On Unix-like systems:
- fork() creates a new process (a copy of the current process).
- exec() replaces the process image with a new program.
- wait() pauses the parent until the child finishes.

On Windows systems:
- CreateProcess() is used to create a new process.

### Example:

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();  // Create a new process

    if (pid == 0) {
        // Child process
        printf("Hello from the child process! PID: %d\n", getpid());
    } else if (pid > 0) {
        // Parent process
        wait(NULL);  // Wait for child to finish
        printf("Hello from the parent process! PID: %d\n", getpid());
    } else {
        // Fork failed
        perror("fork");
        return 1;
    }

    return 0;
}
```
> PID refers to Process ID

Output:

- Hello from the child process! PID: 12345
- Hello from the parent process! PID: 12344
