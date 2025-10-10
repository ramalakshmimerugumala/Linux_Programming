## 1.Explain the concept of process creation in operating systems.
When a new process is created, both the parent and the child get their own memory space in the user space.At the same time, the operating system creates a Process Control Block (PCB) for each process in the kernel space.
The PCB stores important information such as the process ID (PID), parent process ID, file descriptor table, signal disposition table, and page table — which helps the OS manage and control each process.

## 2 Differentiate between the fork() and exec() system calls.
```
         fork()                                                           exec()
1.Used to create a new process (child process).                   1. Used to replace the current process with a new program
2.After fork(), there are two processes – parent and child        2.After exec(), the current process is replaced, so only one process continues.
3.Child gets a copy of the parent’s memory.                       3.The existing memory is replaced with a new program.
4.Returns 0 to the child, and child PID to the parent.            4If successful, it does not return (since the old process is replaced).
```
## 3.
