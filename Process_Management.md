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
## 5. Excel()
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
## 6. Excecl using command line argument
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





