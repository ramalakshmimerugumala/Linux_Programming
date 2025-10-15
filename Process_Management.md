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
## 19.







