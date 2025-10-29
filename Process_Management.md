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
