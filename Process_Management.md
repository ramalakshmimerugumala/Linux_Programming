## 1.Explain the concept of process creation in operating systems.
When a new process is created, both the parent and the child get their own memory space in the user space.At the same time, the operating system creates a Process Control Block (PCB) for each process in the kernel space.
The PCB stores important information such as the process ID (PID), parent process ID, file descriptor table, signal disposition table, and page table — which helps the OS manage and control each process.

## 2 Differentiate between the fork() and exec() system calls.
  Aspect	fork()	exec()
Meaning	Used to create a new process (child process).	Used to replace the current process with a new program.
Result	After fork(), there are two processes – parent and child.	After exec(), the current process is replaced, so only one process continues.
Memory	Child gets a copy of the parent’s memory.	The existing memory is replaced with a new program.
Return value	Returns 0 to the child, and child PID to the parent.	If successful, it does not return (since the old process is replaced).
Use case	Process creation.	Program execution.
Example	pid = fork();	execl("/bin/ls", "ls", NULL);
