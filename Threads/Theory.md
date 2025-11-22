## 1.why we are using pthread_create instead of clone() for creating threads?
```
We use pthread_create() because it is easy, safe, portable, and already handles thread management.
clone() is low-level, difficult, and Linux-only, so it is not used for normal thread creation.
```
## 2.why a stack grows?
```
The stack grows because each time a function is called, a new stack frame is created. 
A stack frame stores:
1. local variables
2. function parameters
3. return address (where the program should continue after the function finishes)
```
## 3.what segments are shared by multiple threads within a process?
```
Multiple threads in the same process share:
1. Code segment (text)
2. Data segment (global and static variables)
3. Heap segment (dynamically allocated memory like malloc)
4. Open files and resources (file descriptors)
Each thread has its own stack, but all other segments are shared.
```
## 4.can you fetch the thread entry point return value in your main thread?
```
Yes, you can fetch the thread’s return value by using the second argument of pthread_join().Yes. In pthreads, the main thread can get the return value of a thread by using pthread_join().
pthread_join() receives the value returned from the thread's start routine.
```
## 5. what happens when main function is invoked?
```
1. Program is loaded into memory
2. Stack is created for the program
3. Global and static variables are initialized
4. argc and argv are prepared (if used)
5. main() gets called and execution begins
```
## 6.what happens when cpu stops executing?
```
When the CPU stops executing a program, it simply switches to another program or goes into a waiting (idle) state until there is more work to do.
1. CPU finishes running your program
2. CPU gives control back to the operating system
3. OS decides what the CPU should do next
    → run another program
    → or wait (idle)
```
## 7.During the context switch, which instruction will be usedto copy the contents of cpu register to your context area of PCB?
```
During a context switch, the OS uses instructions like PUSH and MOV to save the CPU register contents into the PCB’s context area.
```
## 8.How do you create separate process?
```
A separate process is created by using the fork() system call.
fork() makes a new child process that runs independently from the parent process.
```
## 9.How do server create separate thread?
```
A server creates a separate thread by calling pthread_create().
Each time a client connects, the server uses pthread_create() to start a new thread to handle that client.
```
## 10..Advantage of Thread over process?
```
1. Threads are faster to create than processes
2. Threads use less memory than processes
3. Threads share the same address space, so data sharing is easy
4. Context switching between threads is faster than between processes
5. Communication between threads does not need special IPC mechanisms.
Threads are lighter, faster, and share memory — processes are heavier and separate.

```
## 11. .Advantage of process over Thread?
```
1. Processes have separate memory, so they are safer (one cannot crash another)
2. A process bug does not affect other processes
3. Better security and protection because memory is isolated
4. Easier to run on multiple CPUs without shared-data issues
5. No need for synchronization tools like mutexes to avoid race conditions
Processes are safer and isolated, so one process cannot disturb another.
```
## 12 How do you overcome this updation or synchronization issue.when the multiple threads are trying to access the global variables?
```
We overcome the synchronization issue by using a mutex (lock).
A mutex allows only one thread at a time to access the global variable, preventing race conditions.
Use a mutex to protect shared global variables.
```
## 13 How much cpu time is given to user space thread and kernel space thread?
```
A kernel-space thread gets its own CPU time because it is scheduled directly by the OS.
A user-space thread does not get separate CPU time — it shares the CPU time given to its process.
```
## 14 A kernel-space thread gets its own CPU time because it is scheduled directly by the OS. A user-space thread does not get separate CPU time — it shares the CPU time given to its process.
```
A kernel-space thread gets its own CPU time because it is scheduled directly by the OS.
A user-space thread does not get separate CPU time — it shares the CPU time given to its process.
```
## 15 Explain POSIX and system-v difference?
```
| POSIX                            | System-V                              |
| -------------------------------- | ------------------------------------- |
| It is a portability standard     | It is a UNIX operating system variant |
| Defines how APIs should behave   | Defines how System-V UNIX behaves     |
| Portable across systems          | Specific to System-V family           |
| POSIX IPC: pthreads, mutex, mmap | System-V IPC: msgget, semget, shmget  |
| Modern and widely used           | Older, legacy style                   |
```
## 16 .what are the points to remember when mutex locks are used to protect the critical section?
```
1. Always lock the mutex before entering the critical section
2. Always unlock the mutex after leaving the critical section
3. Only one thread can hold the mutex at a time
4. Do not hold the mutex longer than necessary
5. Avoid calling sleep(), I/O, or blocking operations while holding the mutex
6. Always ensure the mutex is unlocked even if an error occurs
7. Locking order must be consistent to avoid deadlock
8. Shared data must only be accessed when mutex is locked.

Lock before accessing shared data, unlock after, and avoid deadlocks.

```
## 17 By using mutex_lock what you are acheiving?
```
mutex_lock gives mutual exclusion — one thread at a time.
```
## 18 .Difference between mutex locks and semaphore?
```
| **Mutex**                                              | **Semaphore**                                               |
| ------------------------------------------------------ | ----------------------------------------------------------- |
| Used when **only one thread** should access a resource | Used when **multiple threads** can access a resource        |
| Has **ownership** – the same thread must unlock it     | **No ownership** – one thread can lock, another can unlock  |
| Always **binary (1 or 0)**                             | Can be **binary or counting** (0 to N)                      |
| Used mainly for **mutual exclusion**                   | Used mainly for **synchronization and resource management** |
| Simpler to use                                         | Slightly more complex                                       |
| Example: one bathroom key shared among people          | Example: parking lot with limited number of slots           |
```
## 19 


