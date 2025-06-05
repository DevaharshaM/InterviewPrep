# Inter-Process Communication (IPC) and Synchronization

**Inter-Process Communication (IPC)** refers to the mechanisms that allow processes to **exchange data** and **coordinate execution**. It's essential in multitasking systems where processes often need to share resources or data.

To safely manage shared access and avoid race conditions, the OS provides **synchronization mechanisms** like semaphores and mutexes.

---

## Synchronization Mechanisms

### 1. Pipes

Used to pass data in a **unidirectional stream** between related processes (typically parent and child).

#### Anonymous Pipe (Unix/Linux)

```c
int pipefd[2];
pipe(pipefd); // pipefd[0]: read end, pipefd[1]: write end

if (fork() == 0) 
{
    close(pipefd[0]);
    write(pipefd[1], "hello", 5);
} 
else 
{
    close(pipefd[1]);
    char buf[6];
    read(pipefd[0], buf, 5);
    buf[5] = '\0';
    printf("%s\n", buf);
}
```
#### Named Pipe (FIFO)

```bash
mkfifo mypipe
echo "hello" > mypipe
cat < mypipe
```

### 2. Message Queues

Provides asynchronous communication using message buffers. More flexible than pipes.

Example (System V):

```c
struct msgbuf 
{
    long mtype;
    char mtext[100];
};

msgsnd(msgid, &msg, sizeof(msg), 0);
msgrcv(msgid, &msg, sizeof(msg), 1, 0);
```

### 3. Semaphores

A semaphore is a signaling mechanism that controls access to shared resources.

#### Types:

| Type     |	Value Range	| Use Case                  |
|----------|--------------|---------------------------|
| Binary	 | 0 or 1       |	Acts like a lock          |
| Counting |	≥ 0	        | Manage multiple resources |

##### Binary Semaphore Example

```c
sem_t sem;
sem_init(&sem, 0, 1);

sem_wait(&sem);   // enter critical section
// ... critical section ...
sem_post(&sem);   // leave critical section
```

##### Counting Semaphore Example

```c
sem_t sem;
sem_init(&sem, 0, 3); // allow 3 simultaneous accesses

sem_wait(&sem);
// critical section
sem_post(&sem);
```

### 4. Mutex (Mutual Exclusion)

A mutex allows only one thread or process to access a critical section at a time.

#### Example (POSIX Threads)

```c
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

pthread_mutex_lock(&lock);
// critical section
pthread_mutex_unlock(&lock);
```
---

## Synchronization Issues

1. Race Condition

Occurs when multiple processes access shared data concurrently, leading to unpredictable results.

2. [Deadlock](https://github.com/DevaharshaM/InterviewPrep/blob/realtimeOS/Process-Task%20Management/Deadlock%20and%20other%20issues.md)

Happens when two or more processes wait indefinitely for each other to release resources.

3. Starvation

A process waits too long to acquire a resource due to biased scheduling.

4. Priority Inversion

A low-priority process holds a resource needed by a higher-priority one, potentially stalling the system.

---

## Summary

| Mechanism     |	Scope              | Blocking? |	Common Use Case                   |
|---------------|--------------------|-----------|------------------------------------|
| Pipe	        | IPC (parent-child) | Yes	     | One-way data flow                  |
| Message Queue |	IPC	               | No	       | Asynchronous messaging             |
| Semaphore	    | IPC/Threads	       | Yes	     | Access control, producer-consumer  |
| Mutex	        | Threads only	     | Yes	     | Critical section protection        |
