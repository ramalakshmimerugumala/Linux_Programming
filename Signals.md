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
1️⃣ signal(SIGINT, mysighandler) changes the default behavior of SIGINT, so pressing Ctrl + C will no longer terminate the program.
2️⃣ Instead, it will simply call your handler function and print the message.
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
## 


