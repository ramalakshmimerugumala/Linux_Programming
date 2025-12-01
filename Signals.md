## 1.signal
```
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
void mysighandler(int signo){
        printf("My signal number %d",signo);
}
int main(){
        signal(SIGINT,mysighandler);
        while(1){
           printf("Sleeping\n");
           sleep(1);
        }
}
1️ signal(SIGINT, mysighandler) changes the default behavior of SIGINT, so pressing Ctrl + C will no longer terminate the program.
2️ Instead, it will simply call your handler function and print the message.
```
## 2. SIGACTION
```
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
#include <stdlib.h>
void sighandler(int signo){
        printf("My signalhandler %d",signo);
        exit(0);
}
int main(){
 struct sigaction act;
 act.sa_handler=sighandler;
 act.sa_flags=0;
 sigemptyset (&act.sa_mask);
 sigaction(SIGINT, &act,NULL);
 while(1){
         printf("Hello world\n");
         sleep(1);
    }
}
```
## 1.Write a C program to catch and handle the SIGINT signal
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo){
        printf("caught signal=%d\n",signo);
}
int main(){
 signal(SIGINT,handler);
 while(1){
         printf("Hello\n");
         sleep(1);
     }
}
```
## 2.Implement a C program to send a custom signal to another process
```
Receiver Program
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void sighandler(int signo){
  printf("Sinal numbr=%d",signo);
  exit(0);
}
int main(){
  signal(SIGUSR1,sighandler);
  printf("Receiver running pid=%d\n",getpid());
  while(1){
   printf("Sleeping\n");
   sleep(1);
  }
}
```
Sender program
```
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
#include <stdlib.h>
int main(int argc, char *argv[]){
  if(argc!=2){
          printf("usage=%s",argv[0]);
  }
  int pid;
  pid=atoi(argv[1]);
  if(kill(pid,SIGUSR1)==0){
          printf("Signal sent to process %d\n",pid);
  }
  else{
          perror("Error in sending signals");
  }
}
```
## 3.Create a C program to ignore the SIGCHLD signal temporarily
```
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>
#include <sys/types.h>
int main(){
 signal(SIGCHLD,SIG_IGN);
pid_t pid=fork();
if(pid==0){
 printf("Child Process..\n");
 sleep(1);
 printf("child pid= %d",getpid());

}
else if(pid>0){
        printf("Parent process pid=%d\n",getpid());
        sleep(3);
}
else{
  perror("Fork failed");
}
}
```
## 4 Write a program to block the SIGTERM signal using sigprocmask()
```
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
int main(){
sigset_t set;
sigemptyset(&set);
sigaddset(&set,SIGTERM);
//sigaddset(&set,SIGINT);
if(sigprocmask(SIG_BLOCK,&set,NULL)==-1){
        perror("sigprocmask");
        return 1;
}
printf("sigterm is blocked.. pid=%d\n",getpid());
while(1){
 printf("Sleeping..\n");
 sleep(2);
}
return 0;
}
```
kill -15 <PID>
Program does NOT terminate (because SIGTERM is blocked.

## 5Implement a C program to handle the SIGALRM signal using sigaction().
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void signalhandler(int signo){
 printf("signal number=%d\n",signo);
 //alarm(3)// to make cyclic
}
int main(){
struct sigaction act;
 act.sa_handler=signalhandler;
 act.sa_flags=0;
 sigemptyset(&act.sa_mask);
 sigaction(SIGALRM,&act,NULL);
 alarm(3);
 while(1){
   printf("Blocking..\n");
   sleep(1);
}
}
```
## 6.Write a C program to install a custom signal handler for SIGTERM?
```
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
void signalhandler(int signo){
        printf("Signal number=%d",signo);
}
int main(){
 signal(SIGTERM,signalhandler);
 while(1){
   printf("Sleeping..\n");
   sleep(1);
 }
}
```




