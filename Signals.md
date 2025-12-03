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
## 7.Create a program to handle the SIGILL signal (illegal instructio
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo){
 printf("%d ",signo);
}
int main(){
 signal(SIGILL,handler);
 printf("raising SIGILL\n");
 raise(SIGILL);
 while(1){
   printf("Sleeping..\n");
   sleep(1);
}
}
```
## 8.Implement a program to handle the SIGSEGV signal (segmentation fault)
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void sighandler(int signo){
  printf("caught signal=%d",signo);
}
int main(){
struct sigaction act;
act.sa_handler=sighandler;
act.sa_flags=0;
sigemptyset(&act.sa_mask);
sigaction(SIGSEGV,&act,NULL);
  int *ptr=NULL;
   *ptr=10;
  sleep(5);
}
```
## 9.Write a program to handle the SIGABRT signal (abort).
```
#include <unistd.h>
#include <stdio.h>
#include <signal.h>
#include <stdlib.h>
void sighandler(int signo){
    printf("Caught SIGABRT: %d\n", signo);
    _exit(1);
}
int main() {
    struct sigaction act;
    act.sa_handler = sighandler;
    act.sa_flags = 0;
    sigemptyset(&act.sa_mask);
    sigaction(SIGABRT, &act, NULL);
    printf("About to raise SIGABRT...\n");
    sleep(1);
    abort();
    printf("This line will never execute.\n");
    return 0;
}
```
## 10.   Implement a C program to handle the SIGQUIT signal 
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void sighandler(int signo){
    printf("Caught SIGQUIT: %d\n", signo);
}
int main() {
    struct sigaction act;
    act.sa_handler = sighandler;
    act.sa_flags = 0;
    sigemptyset(&act.sa_mask);
    sigaction(SIGQUIT, &act, NULL);
    printf("Running program. Press Ctrl + \\ to send SIGQUIT.\n");
    while(1){
        printf("Sleeping..\n");
        sleep(2);
    }

    return 0;
}
```
## 11.Write a program to handle the SIGWINCH signal (window size change).
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void signalhandler(int signo){
printf("Caught signal=%d",signo);
//signal(SIGWINCH,SIG_DFL);//it prints the default behaviour
//raise(SIGWINCH);
}
int main(){
 signal(SIGWINCH,signalhandler);
 while(1){
  printf("Sleeping\n");
  sleep(1);
}
}
```
## 12 Create a program to handle the SIGPWR signal (power failure restart)
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>
void myhandler(int signo){
 printf("Signal number=%d\n",signo);
}
int main(){
  signal(SIGPWR,myhandler);
  while(1){
          printf("Sleeping..\n");
          sleep(1);
  }
}
```
## 13 Implement a C program to handle the SIGXFSZ signal (file size limit exceeded)
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void handler(int signo){
    printf("Received signal: %d (SIGXFSZ - File size limit exceeded)\n", signo);
}

int main() {
    signal(SIGXFSZ, handler);

    FILE *fp = fopen("test.txt", "w");
    if (!fp) {
        perror("File open failed");
        return 1;
    }

    while (1) {
        fprintf(fp, "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\n");
        fflush(fp);
    }

    fclose(fp);
    return 0;
}
```
## 14.Write a program to handle the SIGSYS signal
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void myhandler(int signo){
 printf("Signal handler=%d\n",signo);
}
int main(){
 signal(SIGSYS,myhandler);
 while(1){
         printf("Hello\n");
         sleep(2);
 }
}
```
## 15 .Implement a C program to handle the SIGINFO signal (status request from keyboard).
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void info_handler(int signo) {
    printf("\nReceived SIGINFO (signal %d): Status requested.\n", signo);
}
int main() {
    // Install handler for SIGINFO
    signal(SIGINFO, info_handler);
    printf("Program running... PID = %d\n", getpid());
    printf("Press Ctrl + T to trigger SIGINFO (on BSD/macOS).\n");
    while (1) {
        printf("Working...\n");
        sleep(2);
    }
    return 0;
}
```
## 16.Create a C program to handle the SIGRTMIN signal (minimum real-time signal).
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo) {
    printf("Received SIGRTMIN signal! (signal number = %d)\n", signo);
}
int main() {
    signal(SIGRTMIN, handler);
    printf("Program running... PID = %d\n", getpid());
    printf("Send using: kill -%d %d\n", SIGRTMIN, getpid());
    while (1) {
        printf("Waiting for SIGRTMIN...\n");
        sleep(2);
    }
    return 0;
}
```
## 17  Implement a program to handle the SIGRTMAX signal (maximum real-time signal)
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

// Signal handler function
void handler(int signo) {
    printf("Received SIGRTMAX signal: %d\n", signo);
}

int main() {
    // Install signal handler for SIGRTMAX
    signal(SIGRTMAX, handler);

    printf("Program running... PID = %d\n", getpid());
    printf("Send SIGRTMAX using: kill -%d %d\n", SIGRTMAX, getpid());

    // Infinite loop to keep the program running
    while (1) {
        sleep(1);
    }

    return 0;
}
```
## 18 Write a program to handle the SIGABRT_ABORT signal (abort signal)
```
#include <stdio.h>
#include <signal.h>
#include <stdlib.h>
#include <unistd.h>

// Signal handler for SIGABRT
void handler(int signo) {
    printf("Received SIGABRT signal: %d\n", signo);
    // You can choose to exit or continue
    exit(1);
}

int main() {
    // Install the custom signal handler for SIGABRT
    signal(SIGABRT, handler);

    printf("Program running... PID = %d\n", getpid());
    printf("You can abort this program by calling abort() or sending SIGABRT\n");

    // Infinite loop to keep program running
    while (1) {
        sleep(1);
    }

    return 0;
}
```
## 19.Create a C program to handle the SIGSEGV_SIGBUS signal (segmentation fault or bus error)
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
#include <stdlib.h>
void handler(int signo) {
    if (signo == SIGSEGV)
        printf("Caught SIGSEGV (Segmentation Fault)!\n");
    else if (signo == SIGBUS)
        printf("Caught SIGBUS (Bus Error)!\n");
    exit(1);
}
int main() {
    signal(SIGSEGV, handler);
    signal(SIGBUS, handler);
    printf("Program running... PID = %d\n", getpid());
    int *ptr = NULL;
    *ptr = 10;
    while(1) {
        sleep(1);
    }

    return 0;
}
```
## 20.. Implement a program to handle the SIGUSR1_SIGUSR2 signal (user-defined signal).
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void myhandler(int signo){
 if(signo==SIGUSR1){
         printf("Received USR1 signal \n");
 }
 if(signo==SIGUSR2){
         printf("Received USR2 signal\n");
}
}
int main(){
signal(SIGUSR1,myhandler);
signal(SIGUSR2,myhandler);
while(1){
        printf("HEllo.\n");
        sleep(1);
}
}
```
## 21 . Create a C program to handle the SIGCONT_SIGSTOP signal (continue or stop executing).
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo) {
    if (signo == SIGCONT) {
        printf("Received SIGCONT → Process continued!\n");
    }
}
int main() {
    signal(SIGCONT, handler);
    printf("Program running... PID = %d\n", getpid());
    printf("You can stop using: kill -STOP %d\n", getpid());
    printf("You can continue using: kill -CONT %d\n", getpid());
    while (1) {
        printf("Working...\n");
        sleep(2);
    }

    return 0;
}
```
## 22 Write a program to demonstrate how to block signals using sigprocmask()
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo){
        printf("Caught signal=%d\n",signo);
}
int main(){
sigset_t set;
sigemptyset(&set);
sigaddset(&set,SIGINT);
if(sigprocmask(SIG_BLOCK,&set,NULL)==-1){
        perror("sigprocmask");
        return 1;
}
printf("SigTerm is blocked.");
while(1){
 printf("Sleeping..\n");
 sleep(1);
}
}
```
## 23  Write a program to implement a timer using signals.
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo){
        printf("%d",signo);
        //alarm(5);
}
int main(){
 signal(SIGALRM,handler);
 alarm(5);
 printf("Time expies..");
 while(1){
   printf("Timer.\n");
   sleep(1);
 }
}
```
## 24 Why we use raise system call explain it programmatically
raise() is used to send a signal to the same process itself.
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo) {
    printf("Caught signal = %d\n", signo);
}
int main() {
    signal(SIGUSR1, handler);
    printf("I am going to raise SIGUSR1...\n");
    raise(SIGUSR1);
    printf("Signal handled successfully!\n");
    return 0;
}
```
## 25 Write a c program on pause system call
```
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
void handler(int signo) {
    printf("Signal received = %d\n", signo);
}
int main() {
    signal(SIGUSR1, handler);
    printf("Program waiting... PID = %d\n", getpid());
   // printf("Send signal using: kill -10 %d\n", getpid());
    pause();
    printf("Program resumed after signal.\n");
    return 0;
}
```
## 26 
