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
## 3.Write a C program to demonstrate the use of fork() system call
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
int main(){
 int pid=fork();
 if(pid<0){
   printf("Fork failed");
}
else if(pid==0){
        printf("Child process.\n");
        printf("child PID:%d\n",getpid());
        exit(1);
}
else{
        printf("Parent process.\n");
        printf("parent PID:%d\n",getpid());
        printf("Child from Parent pid:%d\n",pid);

}
}
```
## 4.Write a C program to create multiple child processes using fork() and display their PID
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
int main(){
        int n;
        printf("Enter number of child process");
        scanf("%d",&n);
  for(int i=0;i<n;i++){
          int pid=fork();
  if(pid<0){
          printf("Fork failed");
  }
  else if(pid==0){
          printf("Child Process\n");
          printf("PID of child process:%d\n",getpid());
          exit(1);
  }
  else{
  }
  }
  printf("Parent process PID:%d\n",getpid());
}
output
Enter number of child process3
Child Process
PID of child process:3725
Parent process PID:3724
Child Process
PID of child process:3726
Child Process
PID of child process:3727
```
## 5. Execl()
```
#include <stdio.h>
#include <unistd.h>
int main(){
int ret;
printf("I an going to execute the ls command\n");
ret=execl("/bin/ls","ls","-l",NULL);
printf("I am executing");
}
output
I an going to execute the ls command
total 36
-rwxrwxr-x 1 ramalakshmi ramalakshmi 16048 Oct 10 22:09 a.out
-rw-rw-r-- 1 ramalakshmi ramalakshmi   290 Oct 10 22:09 execel.c
-rw-rw-r-- 1 ramalakshmi ramalakshmi   411 Oct 10 08:01 execv.c
-rw-rw-r-- 1 ramalakshmi ramalakshmi   343 Oct 10 21:58 fork.c
-rw-rw-r-- 1 ramalakshmi ramalakshmi   391 Oct 10 21:58 multiple_child.c
-rw-rw-r-- 1 ramalakshmi ramalakshmi   775 Oct 10 22:04 multiple_child_PID.c
```
## 6. Execl using command line argument
```
#include <stdio.h>
int main(int argc,char *argv[]){
        for(int i=0;i<argc;i++){
                printf("%s\n",argv[i]);
        }
}
output
ramalakshmi@ramalakshmi-VirtualBox:~/linux/processmanagement$ ./a.out viven hyderabad
./a.out
viven
hyderabad
```
## 7.Execv
```
#include <stdio.h>
#include <unistd.h>
int main(){
int ret;
char *argv[]={"ps","-ef",NULL};
printf("I am executing ps command\n");
execv("/bin/ps",argv);
printf("Executed successfully");
}
```
## 8 Discuss the significance of the getpid() and getppid() system calls
```
getpid() → returns the PID of the current process.
getppid() → returns the PID of the parent process (the one that created this process).
```
## 9.Explain the concept of process termination in UNIX-like operating systems
```
Normal finish – program reaches the end.
exit() – program stops with a status code.
kill – stopped by OS or another process.
```
## 10. Describe the process hierarchy in UNIX-like operating systems.
```
What is it?
UNIX processes are organized in a tree structure.
Every process (except the very first) has a parent process and can have child processes.
Main points:
The first process in UNIX is called init (or systemd in modern Linux). Its PID = 1.
Parent process → creates child processes using fork().
Each process knows its PID (process ID) and PPID (parent process ID).
Child processes can create their own children, forming a tree.
# All processes form a tree.
init is the root.
Processes can have parents and children.
Use PID and PPID to see the relationships
```
## 11.What is the purpose of the exit() function in C programming?
```
When you call exit(), it stops the entire program immediately.
Nothing after exit() gets executed.
It also returns a status code to the operating system and cleans up resources like closing files or freeing memory.
```
## 12. Difference between return and exit
```
+----------------------+------------------------------+------------------------------+
| Feature              | return in main()             | exit()                       |
+----------------------+------------------------------+------------------------------+
| What it does         | Ends the main() function     | Ends the whole program       |
+----------------------+------------------------------+------------------------------+
| Where it can be used | Only inside functions        | Anywhere in the program      |
+----------------------+------------------------------+------------------------------+
| Cleanup              | Normal cleanup in main       | Cleans up files & buffers    |
+----------------------+------------------------------+------------------------------+
| Exit status          | Returns value to OS (0/1)   | Sends status code to OS      |
+----------------------+------------------------------+------------------------------+
| Effect on code after | Code after return not run    | Code after exit() never runs |
+----------------------+------------------------------+------------------------------+
```
## 13 Discuss the role of the fork() system call in implementing multitasking
```
Multitasking = running multiple processes at the same time.
fork() allows the OS to create new processes dynamically.
Each process can run different tasks or the same program with different data.
Example: A shell uses fork() to run commands in separate processes while the shell continues running
```
## 14.How does the exec() system call replace the current process image with a new one?
```
Replaces current program with a new program.
Control starts at the new program’s main().
Command-line arguments (argv) go to the new program.
PID stays the same; only the program changes.
Code after exec() does not run if exec succeeds.
```
## 15.Explain the concept of process scheduling in operating systems
```
What it is:
Deciding which process runs next on the CPU.
Who decides:
The OS scheduler decides based on some rules or algorithms.
Why it’s needed:
CPU can run only one process at a time.
Multiple processes may be ready to run.
Scheduling ensures fairness, efficiency, and multitasking
```
## 16.Describe the role of the clone() system call in process management
```
clone() is a system call in Linux used to create a new process or thread.
It’s more powerful and flexible than fork().
clone() allows you to control what resources are shared between parent and child, which is important for multithreading.
```
## 17 Write a program in C to create a zombie process and explain how to avoid it.
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(){
   int pid=fork();
   if(pid>0){
           printf("Parent process.\n");
           printf("Parent process PID=%d\n",getpid());
           printf("child PID in parentprocess=%d\n",pid);
           sleep(100);
   }
   else if(pid==0){
           printf("Child process\n");
           printf("Child process PID=%d\n",getpid());
           exit(0);
   }
}
how to avoid
by using wait or waitPID in parent
```
## 18 Discuss the significance of the setuid() and setgid() system calls in process man
```
These are system calls used to change the user ID (UID) and group ID (GID) of a process.
They help in controlling permissions and security in UNIX/Linux systems.
Setuid() – Set User ID
Syntax:
int setuid(uid_t uid);
setgid() – Set Group ID
Syntax:
int setgid(gid_t gid);
```
## 19.Explain the concept of process groups and their significance in UNIX-like operating systems.
```
A process group is a set of processes that are related to each other and work together as a single unit
The significance of process groups is that they make it easy to control, signal, and manage multiple related processes together — especially for job control in terminals.
```
## 20.Write a C program to demonstrate the use of the waitpid() function for process synchronization
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
int main(){
pid_t pid1,pid2;
int status;
pid1=fork();
if(pid1<0){
        perror("Failure");
}
if(pid1==0){
        printf("Child process 1.\n");
        printf("Child 1 PID=%d\n",getpid());
        sleep(2);
        printf("child 1 Executed");
  exit(2);
}
pid2=fork();
if(pid2<0){
        perror("Falure");
}
if(pid2==0){
        printf("Child process 2\n");
        printf("Child 2 PID=%d\n",getpid());
       sleep(1);
      printf("Child 2 is executed..");
       exit(1);
}
printf("parent process waiting for second child.\n");
waitpid(pid2,&status,0);
printf("Child2 completed its execution with the Exit status=%d\n",WEXITSTATUS(status));
printf("Parent is waiting for first child.\n");
waitpid(pid1,&status,0);
printf("Child1 completes its execution with the Exit stattus=%d\n",WEXITSTATUS(status));
printf("Child 1 completed its execution\n");
}
output
Child process 1.
Child 1 PID=7806
parent process waiting for second child.
Child process 2
Child 2 PID=7807
Child 2 is executed..Child2 completed its execution with the Exit status=1
Parent is waiting for first child.
child 1 ExecutedChild1 completes its execution with the Exit stattus=2
Child 1 completed its execution
```
## 21.Discuss the role of the execle() function in the exec() family of calls.
```
The execle() system call loads and executes a new program in place of the current running process.
Once it executes successfully, the old program is completely replaced by the new one — only the process ID (PID) remains the same.
```
## 22.Describe the purpose of the nice() system call in process scheduling
```
By using the nice() system call, we can change the priority of a process.
Higher nice value → Lower priority (process runs more slowly or “nicely”)
Lower nice value → Higher priority (process runs faster or gets more CPU time)
The range of nice values is:
 -20 to +19
-20 → Highest priority (most aggressive, gets more CPU time)
+19 → Lowest priority (most polite, gets less CPU time)
Syntax:
int nice(int inc);
inc → The increment value added to the process’s current nice value.
A higher nice value → process runs more politely (lower priority).
A lower nice value → process runs less politely (higher priority).
```
## 23.Write a program in C to create a daemon process
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int main(){
        pid_t pid;
        pid=fork();
  if(pid<0){
          printf("Failure");
          exit(1);
  }
  if(pid>0){
          printf("Parent process :%d\n",getpid());
          exit(2);
  }
   if(setsid()<0){
          exit(1);
  }
  chdir("/");
  umask(0);
  close(STDIN_FILENO);
  close(STDOUT_FILENO);
  close(STDERR_FILENO);
  while(1){
          sleep(5);
  }
  return 0;
}
output
Parent process :4255
to see the demon process in background--
ps -ef |grep ./a.out
ramalak+    4215    2142  0 11:12 pts/0    00:00:00 ./a.out
ramalak+    4228    2142  0 11:14 pts/0    00:00:00 ./a.out
ramalak+    4256    2142  0 11:16 ?        00:00:00 ./a.out
ramalak+    4270    3542  0 11:19 pts/0    00:00:00 grep --color=auto ./a.out
## to kill the demon process
pkill a.out
```
## 24.Write a C program to demonstrate the use of the system() function for executing shell commands 
```
The system() function in C is used to execute Linux or shell commands directly through a C program.

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
int main(){
        printf("Demonistrate the use of system function\n");
        printf("Listing all the files\n");
        system("ls");
        printf("Displaying the current working directory\n");
        system("pwd");
        printf("Showing current date and time\n");
        system("date");
        printf("Displaying the current logged-in \n");
        system("whoami");
}
output
Demonistrate the use of system function
Listing all the files
a.out	  execv    multiple_child.c	 sample       waitpid.c
demon.c   execv.c  multiple_child_PID.c  sample.c     zombie.c
execel.c  fork.c   orphan.c		 systemfun.c
Displaying the current working directory
/home/ramalakshmi/linux/processmanagement
Showing current date and time
Tue Oct 28 11:42:59 AM IST 2025
Displaying the current logged-in 
ramalakshmi
```
## 25 Explain the concept of process states in UNIX-like operating systems
```
In UNIX-like systems, a process goes through several states during its lifetime. These states describe the current condition of the process.
1. New
The process is being created.
Memory is allocated in user space, and a Process Control Block (PCB) is initialized in kernel space.
2. Ready
The process is ready to run but waiting for CPU time.
It is placed in the ready queue by the scheduler.
When the CPU becomes available, it moves to the running state.
3. Running
The process is currently being executed by the CPU.
Instructions of the program are active.
4. Blocked (Waiting)
The process is waiting for an event (like I/O operation) to complete.
It cannot continue until the required event occurs.
5. Terminated (Exit)
The process has finished its execution.
All resources are released, and the process is removed from the system.
6. Zombie
The process has finished execution, but its parent process has not yet collected its exit status using wait().
It remains in the process table until the parent reads the exit status
```
## 26. Describe the purpose of the chroot() system call and provide an example.agement
```
chroot is used to change the root directory of current process and its child process.
After this, the process and its children cannot access files outside the new root, making it useful for security isolation or creating sandbox environments.

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
int main(){
        if(chroot("/home/ramalakshmi/linux")==0){
                printf("Changed root directoty successfully..");
        }
        else{
                perror("Failed");
        }
}
```
## 27.Write a C program to create a process using fork() and pass arguments to the child process 
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
int main(int argc,char *argv[]){
        pid_t pid;
        pid=fork();
        if(pid<0){
                printf("Fork failed");
        }
        else if(pid==0){
                printf("Child process.\n");
                printf("PID of cild process=%d\n",getpid());
                printf("Arguments received by child..\n");
                for(int i=1;i<argc;i++){
                        printf("%s",argv[i]);
                }
 }
        else{
                printf("Parent process.\n");
                printf("Parent process PID=%d\n",getpid());
        }
}
output
ramalakshmi@ramalakshmi-VirtualBox:~/linux/processmanagement$ ./a.out hi hello how are u 
Parent process.
Parent process PID=6575
Child process.
PID of cild process=6576
Arguments received by child..
hihellohowareu
```
## 28 Explain the significance of process identifiers (PIDs) in process management
```
A Process Identifier (PID) is a unique number assigned by the operating system to every running process.
It helps the OS and users to identify, manage, and control individual processes.
```
## 29.Discuss the concept of orphan processes and how they are handled in UNIX-like operating systems
```
In an orphan process, the parent process terminates first while the child process is still running.
When this happens, the child process is adopted by the first process, known as the init process, whose PID is 1.
The init process becomes the new parent of the orphan process and takes care of it until it finishes execution
```
## 30. Describe the concept of process priority and how it is managed in operating systems
```
Process priority decides which process gets CPU time first. Every process is assigned a priority value, and the CPU scheduler uses it to determine the order of execution..
How It Is Managed
In UNIX/Linux, process priority is managed using the nice value.
The nice value ranges from –20 to +19:
Lower nice value (–20) → Higher priority (process runs first).
Higher nice value (+19) → Lower priority (process runs later).
nice → set priority when starting a process.
renice → change priority of a running process.
```
## 31.Explain the purpose of the fork() system call in creating copy-on-write (COW) processes
```
When a new process is created using the fork() system call, both the parent and the child initially share the same memory pages — this is known as Copy-on-Write (COW).
They share the same pages as long as they perform only read operations.
When either process performs a write operation, the operating system creates a separate copy of the page for that process, ensuring data independence and efficient memory usage
```
## 32.Discuss the role of the execvp() function in searching for executable files.
```
execvp() is used to replace the current program with a new program.
If the given argument does not contain a slash (/), it searches for the executable file in the directories listed in the PATH environment variable.
If the argument contains a slash (/), it is treated as a path, and execvp() directly tries to execute that file.

#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>
int main(){
   char *argv[5];
   argv[0]="ps";
   argv[1]="-ef";
   argv[2]=NULL;
   execvp("ps",argv);
}
```
## 33.Write a C program to demonstrate the use of the execvpe() function
```
```
## 34. Explain the concept of process context switching and its impact on system performance
```
Context switching means the CPU stops executing the current process, saves its state, and loads the state of another process to share the CPU time among multiple processes.
Context switching is mainly used in multitasking and time-sharing systems to make multiple processes appear to run simultaneously..
```
## 35.Discuss the role of the clone() system call in creating threads in Linux.
```
In Linux, threads are implemented using the clone() system call.
By passing specific flags (like CLONE_VM, CLONE_FS, CLONE_FILES, CLONE_SIGHAND), the new task shares the same memory and resources with the calling process.
This allows multiple threads to run in the same address space, making communication between them fast and efficient.

The clone() system call is similar to fork() but more flexible.
It is mainly used to create threads in Linux because it allows the new thread to share the same memory and resources with the parent process
```
## 36 Write a C program to create a process group and change its process group ID (PGID).
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
int main(){
 pid_t pid;
 pid=fork();
 if(pid<0){
         printf("Failure of fork");
 }
 if(pid==0){
         printf("Child process..\n");
         printf("Before changing the process group Id\n");
         printf("Child process PID=%d\n,Group process(GPID)=%d\n",getpid(),getpgrp());

 if(setpgid(0,0)==0){
 printf("After changing the process Group id\n");
         printf("Child PID=%d\n,Process Group Id=%d\n",getpid(),getpgrp());
 }
 else{
    perror("setpgid failed");
 }
 }
 else{
         printf("Parent process\n");
         printf("Parent Process PID=%d\n,Group ID=%d\n",getpid(),getpgrp());sleep(2);

 }
}
output
Parent process
Child process..
Before changing the process group Id
Parent Process PID=9142
,Group ID=9142
Child process PID=9143
,Group process(GPID)=9142
After changing the process Group id
Child PID=9143
,Process Group Id=9143
```
## 37.Explain the difference between process creation using fork() and pthread_create().
```
Feature	                   fork()	                                                           pthread_create()
Purpose	               Used to create a new process.	                               Used to create a new thread within the same process..
Memory Space       The new process gets a separate copy of the parent’s memory      The new thread shares the same memory and resources with the parent thread
                   (address space).

Communication     Processes need inter-process communication (IPC) like pipes or    Threads can directly communicate since they share the same memory
                  shared memory to exchange data.

Execution          Parent and child run independently after creation                  Threads run concurrently within the same process

Systemcall/Library    fork() is a system call provided by the OS kernel                  pthread_create() is a POSIX thread library function (user-level)

Use Case                Used for process-based multitasking                             Used for thread-based multitasking
```
## 38.. Describe the role of the fork() system call in implementing the shell's job control
```
The fork() system call is used by the shell to create a new process for every command the user runs.
This allows the shell to keep control over jobs — it can run them in background, stop, resume, or terminate them, while still accepting other commands.
```
## 39.Explain the purpose of the execlp() function and provide an example
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(){
char *argv[5];
execlp("ls","ls","-l",NULL);
}
```
## 40 Discuss the significance of the setpgid() system call in managing process groups
```
Setpgid() is a UNIX/Linux system call that allows a process to join or create a process group.
Each process group is identified by a PGID (Process Group ID).
int setpgid(pid_t pid, pid_t pgid);
pid → PID of the target process
pgid → New process group ID to assign
```
## 41 Explain the concept of process priority inheritance and its importance in real-time systems
```
In real-time systems, each process has a priority. Sometimes, a low-priority process may hold a resource (like a file or lock) that a high-priority process needs. The high-priority process has to wait — this is called priority inversion.
To fix this, the system uses priority inheritance. The low-priority process temporarily gets the higher priority so it can finish quickly and release the resource. After that, it returns to its original priority.
Importance:
✅ Prevents priority inversion
✅ Ensures real-time tasks finish on time
✅ Improves system performance and reliability
```
## 42.Write a C program to create a child process using vfork() and demonstrate its usage
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
int main(){
  pid_t pid;
  pid=vfork();
  if(pid<0){
          printf("Vfork failure");
          exit(1);
  }
   else if(pid==0){
          printf("Child process PID=%d\n",getpid());
          _exit(0);
  }
  else{
          printf("Parent process PID=%d\n",getpid());
         printf("Child process finishes its execution");
  }
}
```
## 43.Describe the role of the fork() system call in copy-on-write (COW) mechanism and its benefits
```
The fork() system call is used to create a new process.
This new process is called the child process, and the process that created it is the parent process.

Normally, the child should get a copy of the parent’s memory, but copying everything takes time and memory.

Copy-On-Write (COW):
To save time, both parent and child share the same memory at first.
But they cannot change it (it’s read-only).
If one of them tries to modify something, then the system creates a new copy only for that process.
```
## 44.Explain the concept of process scheduling policies such as FIFO, Round Robin, and Priority scheduling
```
When many processes are waiting to use the CPU, the operating system decides which one to run first. This decision is made using scheduling policies
1.FIFO (First In, First Out)
The process that comes first runs first.
Once it starts, it runs until it finishes.
Example:
If processes come in order P1, P2, P3 → they run in the same order.
✅ Simple and easy
❌ Not fair for long-running processes (others must wait)
2.Round Robin (RR):
Each process gets a small time slice (like 1 second).
If it doesn’t finish, it goes to the end of the queue.
Then the next process gets its turn.
Example:
If you have P1, P2, P3 →
P1 runs for 1 sec → P2 runs → P3 runs → then again P1 (if not finished).
✅ Fair for all processes
✅ Good for multitasking systems
❌ Frequent switching can slow down performance
3. Priority Scheduling
Each process has a priority number.
The higher priority process runs first.
Example:
P1 (priority 2), P2 (priority 5), P3 (priority 1)
→ P2 runs first because 5 is highest.
✅ Used in real-time systems
❌ Low-priority processes may starve (never get CPU)
```
## 45 4. Discuss the significance of the execve() function in process creation and execution.
```
The execve() function is used to run a new program inside the current process.
It replaces the current process’s memory with the new program

#include <stdio.h>
#include <unistd.h>
int main() {
    char *args[] = {"/bin/ls", "-l", NULL};
    execve("/bin/ls", args, NULL);
    perror("execve failed");
    return 0;
}
```
## 46.Write a program in C to demonstrate the use of the nice() system call for adjusting process priority
```
#include <stdio.h>
#include <unistd.h>
#include <sys/resource.h>
int main(){
int old=getpriority(PRIO_PROCESS,0);
printf("Old niece value=%d\n",old);
nice(5);
int new=getpriority(PRIO_PROCESS,0);
printf("new niece value=%d",new);
}
output
Old niece value=0
new niece value=5
```
## 47.Explain the concept of process swapping and its role in memory management.
```
When many processes are running, RAM might become full.
The operating system chooses one process that is not currently needed.
That process is moved (swapped out) to the hard disk (swap area).
When that process is needed again, it is brought back (swapped in) to RAM.
This helps multiple processes share limited memory efficiently..
Role in Memory Management
Swapping helps the operating system manage memory when there are more processes than can fit in RAM.
Functions:
✅ Allows more processes to run simultaneously
✅ Makes efficient use of memory
✅ Helps in multiprogramming (running many programs at once)
Disadvantages:
Slower performance, because swapping involves disk I/O (reading/writing to disk is slower than RAM).
Frequent swapping can cause thrashing (system spends most time moving processes in/out of memory)
```
## 48 Discuss the difference between the fork() and pthread_create() functions in terms of process/thread creation
```
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Feature                      | fork()                                        | pthread_create()                             |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| What it creates              | A new **process** (child process)             | A new **thread** within the same process     |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Memory space                 | Child has a **separate copy** of parent’s memory | Threads **share the same memory space**     |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Communication                | Needs **IPC mechanisms** (pipe, shared memory) | Threads **communicate directly** via shared data |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Resource usage               | **Heavyweight**, uses more system resources    | **Lightweight**, uses fewer resources        |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Execution speed              | **Slower**, new process setup required         | **Faster**, runs in same address space       |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Dependency                   | Child process runs **independently** of parent | Threads are **dependent** on each other      |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Data sharing                 | Data **cannot be shared directly**             | Threads **share data and variables** easily  |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Header file required          | Declared in **<unistd.h>**                    | Declared in **<pthread.h>**                  |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Typical use case             | Used for **creating new processes** (e.g., shells) | Used for **multi-threading** in same process |
+------------------------------+-----------------------------------------------+----------------------------------------------+
| Example of ID returned        | Returns **process ID (PID)**                  | Returns **thread ID (pthread_t)**            |
+------------------------------+-----------------------------------------------+----------------------------------------------+
```
## 49.Describe the purpose of the prctl() system call in process management.
```
prctl() stands for Process Control.
It is a Linux-specific system call used to control and modify certain attributes or behaviors of a process at runtime.
It allows a process to set or get various control parameters related to itself or sometimes its children.

#include <stdio.h>
#include <sys/prctl.h>
#include <string.h>
int main() {
    // Set the process name
    prctl(PR_SET_NAME, "MyProcess", 0, 0, 0);
    // Get the process name
    char name[16];
    prctl(PR_GET_NAME, name, 0, 0, 0);
    printf("Process name: %s\n", name);
    return 0;
}
```
## 50.Explain the concept of process preemption and its impact on system responsiveness
```
When Process A is running and a new process B arrives with a higher priority,
the operating system will preempt (pause) Process A and switch the CPU to run Process B immediately.
Once Process B finishes its execution, the CPU will resume Process A from the exact point where it was stopped earlier.
Impact on System Responsiveness (Short Version)
Improves Responsiveness:
CPU quickly switches to high-priority tasks, making the system react faster to user actions.
Better Multitasking:
Allows many programs to run smoothly by sharing CPU time.
Fair CPU Use:
Ensures all processes get a fair share of CPU time.
Small Overhead:
Frequent switching causes slight delay, but overall system stays responsive.
```
## 51.Discuss the role of the exec functions in handling file descriptors during process execution
```
exec() keeps open files and pipes active unless they are marked to close.
This allows smooth communication between old and new programs.
All open file descriptors (like files, pipes, standard input/output) stay open after exec() by default.
This helps the new program continue using the same files or communication channels.
If a file descriptor has the close-on-exec flag (FD_CLOEXEC), it will be closed automatically when exec() runs.
```
## 52.Explain the significance of process priorities and how they affect scheduling decisions
```
Process priority decides which process runs first.
Higher priority = runs sooner.
Lower priority = waits longer.
This ensures the CPU handles important tasks quickly and keeps the system responsive.
```
## 53.Describe the process of process termination and the various ways it can occur
```
Process Termination
It means ending a process when its work is done or something goes wrong.
Ways a process can end:
Normal termination – finishes work and exits normally.
Abnormal termination – ends due to an error (like divide by zero).
Killed by another process – stopped using commands like kill or Ctrl + C.
Parent ends – if parent stops, child may also end.
Zombie/Orphan – special cases when parent or child ends first.
```
## 54. Discuss the role of the exit status in process termination and how it can be retrieved by the parent process
```
When a process finishes, it returns an exit status (exit code) to the operating system.
This exit status tells whether the process ended normally or with an error.
The parent process uses the wait() or waitpid() system call to get the child’s exit status.
The OS stores the exit status temporarily until the parent collects it..
Example:
pid_t pid = fork();
if(pid == 0)
    exit(5);        // child process ends with status 5
else {
    int status;
    wait(&status);  // parent waits for child
    printf("%d", WEXITSTATUS(status)); // prints 5
}
```
## 55.Write a C program to demonstrate process synchronization using the fork() and wait() system calls
```
Synchronization = orderly execution of processes to avoid conflicts and maintain correct results.
In fork() and wait():
The child process runs first.
The parent process uses wait() to synchronize — it waits until the child is done.
This ensures proper order of execution..

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
int main(){
    pid_t pid;
    pid=fork();
    if(pid<0){
        printf("Error in fork");
    }
    if(pid==0){
        printf("Child Process..\n");
        sleep(2);
        exit(5);
        }
        else{
            int status;
            printf("Parent Process...\n");
            wait(&status);
printf("Child Exited with the status =%d\n",WEXITSTATUS(status));   
        }
}
```
## 56 Explain the concept of process suspension and resumption using signals
```
In an operating system, process suspension means temporarily stopping a process’s execution.
Resumption means continuing that stopped process again.
This can be done using signals — special messages sent by the OS or another process.
```
## 57.Discuss the role of process scheduling algorithms in determining the order of execution among processes
```
Main Role of Scheduling Algorithms
Determine Execution Order
Decide which process gets the CPU first, next, and so on.
Ensures that every process gets a fair share of CPU time.
Maximize CPU Utilization
Keeps the CPU busy as much as possible (no idle time).
Reduce Waiting Time & Turnaround Time
Chooses an order that minimizes how long processes wait in the queue.
Improve System Responsiveness
For interactive systems, ensures that short or urgent tasks run quickly.
Ensure Fairness
Makes sure no process is starved (ignored for too long).
```
## 58.Explain the concept of process migration and its relevance in distributed systems.
```
Process migration means moving a running process from one machine to another in a network (distributed system).
Example:
If Server A is overloaded,
one of its running processes can be moved to Server B,
so it can keep running there without restarting.
Why It’s Useful:
Balances the workload between servers.
Improves performance.
Prevents system failure due to overload.
Makes better use of resources.
```
## 59.Describe the role of process identifiers (PIDs) in process management and their uniqueness within the system
```
A Process Identifier (PID) is a unique number that the operating system assigns to every process running in the system.
It acts like an ID card for each process.
Each process has a unique PID that helps the OS identify and manage it. Using the PID, system calls like kill() or wait() can control specific processes. PIDs also connect parent and child processes (getppid() gives the parent’s ID). The OS uses PIDs to handle resources like memory or files. Commands like ps, top, and kill use PIDs to monitor and manage running processes
```
## 60.3. Explain the concept of process tracing and its importance in debugging and monitoring
```
Process tracing means watching how a process runs — step by step — to see what system calls it makes and what data it uses. It helps developers understand program behavior, find bugs, and fix errors. Tools like strace and ptrace() in Linux are used for tracing. It’s important for debugging, performance checking, and ensuring a process works correctly..
```
## 61.Describe the concept of process control blocks (PCBs) and their role in process management
```
A Process Control Block (PCB) is a data structure used by the operating system to store all information about a process.It helps the OS keep track of each process’s state and manage switching between processes.
All important information needed by the OS to run, pause, resume, or terminate a process...
A Process Control Block (PCB) typically contains the following key elements:
PID (Process ID): Unique identifier for the process.
Process State: (Running, Ready, Waiting, etc.)
Program Counter: Points to the next instruction to execute.
CPU Registers: Stores current register values.
Memory Management Info: Includes page table or segment table.
File Descriptor Table (FD table): Tracks files opened by the process.
Signal Disposition Table: Defines how the process handles signals (e.g., ignore, handle, terminate).
Accounting Info: CPU time, process priority, etc
```
## 62.Write a C program to demonstrate the use of the prctl() system call to change process attributes..
```
int prctl(int option, unsigned long arg2, unsigned long arg3,
          unsigned long arg4, unsigned long arg5);
That means prctl() can take up to 5 arguments —
the first one (option) tells what action to perform,
and the next four are optional parameters, whose meanings depend on the option you use.
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/prctl.h>
int main(){
 char name[25];
 prctl(PR_SET_NAME,"NewProcess",0,0,0);
 prctl(PR_GET_NAME,name,0,0,0);
 printf("Process name=%s\n",name);
 printf("Process PID=%d\n",getpid());
}
```
## 63.Explain the concept of process scheduling classes and their significance in real-time operating system
```
A scheduling class is a category of processes that share the same scheduling policy.
Each class has its own rules to decide which process gets the CPU next..
Types of Scheduling Classes:
Normal (Time-Sharing) Class:
Used for regular user processes.
Tries to give fair CPU time to all.
Example: Round Robin, Priority Scheduling.
Real-Time Class:
Used for tasks that must finish on time.
Higher priority than normal processes.
Example: SCHED_FIFO, SCHED_RR in Linux.
```
## 64.Discuss the role of the vfork() system call in process creation and its differences from fork()
```
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Feature                      | fork()                                        | vfork()                                       |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| What it creates              | A new **process** (child process)             | A new **process**, but shares memory with parent |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Memory space                 | Child gets a **copy** of parent’s memory       | Child **shares** parent’s memory temporarily   |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Parent execution             | Parent and child run **independently**        | **Parent is suspended** until child calls exec() or _exit() |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Speed                        | **Slower**, copies entire memory space         | **Faster**, no memory copy                    |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Memory efficiency            | **Consumes more memory**                      | **Uses less memory** (shared temporarily)     |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Use case                     | For general process creation                  | When child **immediately calls exec() or _exit()** |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Data sharing                 | Data **not shared** between parent and child  | Data **shared**, so changes affect parent     |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Header file required          | Declared in **<unistd.h>**                   | Declared in **<unistd.h>**                    |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Example of ID returned        | Returns **process ID (PID)**                 | Returns **process ID (PID)**                  |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
| Dependency                   | Parent and child are **independent**          | Child must call **exec() or _exit()** before parent resumes |
+------------------------------+-----------------------------------------------+-----------------------------------------------+
````
## 65 Describe the purpose of the sigaction() system call in handling signals in processes
```
sigaction() is used to change or modify signal behavior.
It gives more control than the old signal() function.
It is used for safe and reliable signal handling in processes.
```
## 66 Discuss the role of the sigprocmask() system call in managing signal masks for processes
```
The sigprocmask() system call is used to block or unblock signals in a process by changing its signal mask.
Block signals → Temporarily stop certain signals from interrupting the process.
Unblock signals → Allow blocked signals to be delivered again.
Check current mask → Find which signals are currently blocked
int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);
how → Tells what action to perform (SIG_BLOCK, SIG_UNBLOCK, or SIG_SETMASK).
set → The new set of signals to block/unblock.
oldset → Saves the previous mask (optional).
```
## 67 Describe the purpose of the setrlimit() system call in setting resource limits for processes
```
setrlimit() sets resource usage limits for a process.
Prevents any process from overusing system resources.
Helps in system stability and security.
Types of Limits:
Soft limit: The current limit the process can use (can be changed anytime).
Hard limit: The maximum limit that even the process owner cannot exceed easily.
int setrlimit(int resource, const struct rlimit *rlim);
resource → Type of resource (like CPU time, file size, etc.).
rlim → A structure that defines the soft and hard limits.
```
## 68.Discuss the concept of process groups and their importance in job control and signal propagation
```
A process group is a collection of one or more processes that are related and can be controlled together.
Every process in Linux belongs to exactly one process group, identified by a Process Group ID (PGID).
Process groups are mainly used for:
Job control (in shells like bash).
Signal propagation (sending signals to multiple related processes
1.Job Control
When you run a command in a terminal (like ls | grep txt), several processes are created.
These processes are grouped into one process group.
The shell can then pause, resume, or terminate the entire group at once (for example, using Ctrl+Z to stop or fg to continue).
This makes background and foreground job control possible.
2️ Signal Propagation
When a signal (like SIGINT from Ctrl+C) is sent to a process group,
all processes in that group receive the same signal.
This ensures that related processes (like a pipeline) can be stopped or killed together.
```
## 69.Explain the role of the prlimit() system call in setting resource limits for processes.
```
prlimit() is used to get or set resource limits for any process.
 It combines both getrlimit() and setrlimit() in one call.
 Helps the OS control resource usage and prevent overload.
 Useful for monitoring and managing running processes safely.
int prlimit(pid_t pid, int resource,
            const struct rlimit *new_limit,
            struct rlimit *old_limit);
pid → Process ID (use 0 for the current process).
resource → Type of resource (e.g., RLIMIT_CPU, RLIMIT_FSIZE, etc.).
new_limit → New limits to set (or NULL if not changing).
old_limit → Gets the old limits (or NULL if not needed)
```
## 70.Discuss the concept of process scheduling policies in multi-core systems and their implications
```
Definition:
Process scheduling in multi-core systems decides which process runs on which core and for how long to ensure efficient CPU use and better performance.
Main Scheduling Policies:
1.Symmetric Multiprocessing (SMP):
All cores are treated equally.
Each core has its own scheduler.
OS balances load across cores.
✅ Efficient and scalable.
❌ Requires synchronization and load balancing.
2.Asymmetric Multiprocessing (AMP):
One core (master) controls all scheduling.
Other cores (slaves) just execute tasks.
✅ Simple design.
❌ Not efficient for many cores.
3.Affinity-Based Scheduling:
A process is kept on the same core to reuse cached data.
✅ Improves performance (cache locality).
❌ Can cause uneven load.
Load Balancing:
Keeps work evenly distributed across all cores.
Prevents some cores from being overloaded while others are idle.
Implications:
Better CPU utilization and system performance.
Improved responsiveness and throughput.
Need to manage fairness, cache usage, and synchronization.
Increases scheduling complexity compared to single-core systems.
```
## 71.Describe the role of the setpriority() system call in adjusting process priorities.
```
The setpriority() system call is used to change how important (or urgent) a process is for the CPU.
If you increase its priority (give it a lower nice value, like -10),that process will run first or more often than others.
If you decrease its priority (give it a higher nice value, like +10),that process will run later or less often.
Syntax--int setpriority(int which, int who, int priority);
which → specifies target type (PRIO_PROCESS, PRIO_PGRP, or PRIO_USER)
who → identifies the specific process, group, or user
priority → new nice value
```
## 72.Explain the concept of process scheduling latency and its impact on system responsiveness.
```
Process scheduling latency is the time delay between when a process becomes ready to run and when it actually starts executing on the CPU.
In other words, it’s the waiting time before the CPU starts processing a ready task.
Causes of Scheduling Latency
Too many runnable processes (CPU overload)
High-priority processes occupying CPU time
Context-switching overhead
Interrupt handling delays
Impact on System Responsiveness
High Latency → Poor Responsiveness
The system takes longer to respond to user inputs.
Example: Applications open slowly or the cursor lags.
Low Latency → Better Responsiveness
Processes start quickly after becoming ready.
Example: System reacts immediately to user actions.Inefficient scheduling algorithm.
```
## 73.Discuss the role of the prlimit64() system call in setting resource limits for processes with 64-bit address space
```
The prlimit64() system call in Linux is used to set or get resource limits for a process — specifically designed to support 64-bit address space and large resource values.
It is an extended version of the older setrlimit() and getrlimit() calls, allowing applications to handle larger limits (like file sizes, memory, or CPU time) that exceed 32-bit values.
int prlimit64(pid_t pid, int resource,
              const struct rlimit64 *new_limit,
              struct rlimit64 *old_limit);
Parameters:
pid → Process ID (0 means current process)
resource → Type of limit (e.g., RLIMIT_CPU, RLIMIT_AS, RLIMIT_FSIZE)
new_limit → Pointer to structure defining new limits
old_limit → Pointer to store the old limits..
Role / Use:
Controls resource usage by processes (CPU time, memory, file size, etc.)
Prevents a process from overusing system resources.
Supports 64-bit resource values, allowing management of very large resources in modern systems.
```
## 74 Describe the purpose of the sched_getaffinity() system call in querying the CPU  affinity of a process
```
It’s a system call in Linux that is used to find out which CPU cores a process can run on.
Every process in a computer can be allowed to run on one or more CPU cores.
The set of allowed cores for a process is called its CPU affinity.
Example:
If your system has 4 cores (CPU0, CPU1, CPU2, CPU3),
and one process is allowed to run only on CPU0 and CPU1,
then sched_getaffinity() will show that information.
sched_getaffinity() → checks which CPUs a process can use.
sched_setaffinity() → sets which CPUs a process can use.
```
## 75.Discuss the concept of process checkpointing and its relevance in fault tolerance and process migration
```
Process checkpointing is the technique of saving the current state of a running process (such as its memory, CPU registers, open files, and variables) to a file called a checkpoint file.
This saved state can later be restored to continue execution from the same point — even if the system crashes or the process is moved to another machine.
How It Works:
The operating system or a checkpointing tool takes a snapshot of the process state.
The snapshot is stored on disk.
Later, the process can be restarted (restored) from that snapshot instead of starting over.
Relevance in Fault Tolerance
If a system fails or crashes, the process can be restarted from the last checkpoint instead of beginning from scratch.
This minimizes data loss and computation time.
Example: In long scientific simulations, checkpointing ensures progress isn’t lost if power fails.
Relevance in Process Migration
Checkpointing allows a process to move from one machine to another.
The process is checkpointed on one system and restored on another,
allowing load balancing and efficient resource use in distributed systems
```
## 76 Explain the significance of the /proc filesystem in providing information about processes in Linux
```
The /proc filesystem in Linux is a virtual filesystem located in the root directory that provides real-time information about running processes and system resources.
Each running process has a directory under /proc named by its Process ID (PID) (for example, /proc/1234), which contains details such as the process’s status, memory usage, CPU time, and open files.
Significance:
Provides a simple interface to get process and system details without special tools.
Used by commands like ps, top, htop, and vmstat.
Helps in system monitoring, debugging, and performance analysis.
```
## 77. Discuss the concept of process re-parenting and its implications in process management
```
When a parent process terminates before its child process, the child process is said to become orphaned. In such cases, the init process (PID 1) or sometimes systemd automatically adopts (re-parents) the orphaned process. This mechanism ensures that every running process always has a valid parent.
Implications:
Ensures no process is left without a parent.
Prevents zombie processes by guaranteeing proper cleanup.
Helps maintain process hierarchy and system stability.
```
## 78. what is process and what is the difference between process and program?
```
Program Memory Segments (before execution)
A program (just stored on disk) has the following segments:
Text segment → contains the compiled code (instructions).
Data segment → stores global and static initialized variables.
BSS segment → stores global and static uninitialized variables.
These exist in the executable file — but the program is not yet running.
Process Memory Segments (when running)
When the program is loaded into memory and starts executing (becomes a process),
it gets two more important segments:
Heap → for dynamically allocated memory (e.g., malloc() or new).
Stack → for function calls, local variables, and return addresses
```
## 79.what is the difference between ps and top?
```
ps
Shows the list of running processes only once (at that moment).
It does not update automatically.
You have to run it again to see new data
Top
Shows the running processes continuously (live).
The screen updates every few seconds automatically.
You can see CPU and memory usage changing in real time.
ps = photo of processes (static)
top = video of processes (dynamic)
```
## 80.what are the types of processes we have explain each process breifly?
```
1️⃣.System Process
Meaning: Processes started automatically by the operating system when the system boots up.
They manage hardware and background system tasks.
Example:
systemd or init → starts all other processes after boot.
kthreadd → manages kernel threads
2️⃣.User Process
Meaning: Processes started by you (the user) — like opening apps or running programs.
Example:
Opening Chrome → starts a user process.
Running java HelloWorld → creates a user process.
Think of it like: The tasks you do — open browser, editor, etc.
3️⃣.Foreground Process
Meaning: Process that runs in front of you — it takes input from keyboard and shows output on screen.
Example:
Typing cat file.txt → it shows file content right in your terminal.
Running python script.py → runs in foreground and waits for input/output.
Think of it like: You’re talking directly to the process.
4️⃣.Background Process
Meaning: Process that runs behind the scenes — it doesn’t need your input.
Example:
./long_task.sh &
→ Runs in background. You can still type other commands while it runs.
Think of it like: You’re cooking while your washing machine works automatically in background.
5️⃣.Daemon Process
Meaning: A special background process that runs continuously to provide system services.
It starts at boot time and has no terminal connection.
Example:
sshd → handles login/logout through SSH.
crond → runs scheduled tasks like backups.
cupsd → manages printer services.
Think of it like: A security guard — always running, waiting to serve when needed.
6️⃣ Orphan Process
Meaning: A child process whose parent process ended before the child finished.
The init/systemd process adopts it.
Example:
Suppose you run a script that starts another process and then the script ends —
the second process becomes orphan but keeps running.
Think of it like: A child whose parent left — OS adopts it so it’s not lost.
7️⃣ Zombie Process
Meaning: Process that has finished execution but its parent hasn’t read its exit status yet.
It stays as a small entry in the process table.
Example:
You run a program, it ends, but the parent didn’t call wait() — it becomes a zombie.
In ps output, you’ll see <defunct>.
Think of it like: A ghost — dead, but still listed until it’s properly removed.
```
## 81.In parent process can you access to the exit code of return value of child process (or) in parent process how do you block to get the id of child?
```
Yes!
The parent process can access the exit status (return value) of its child process using the wait() or waitpid() system call.
