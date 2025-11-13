## .Thraed Program
```
#include <stdio.h>
#include <unistd.h>
#include <pthread.h>
void *threadfunc1(void *args);
void *threadfunc2(void *args);
int glob=0;
int main(){
    pthread_t t1;
    pthread_t t2;
    int loop=2000;
    pthread_create(&t1,NULL,threadfunc1,&loop);
    pthread_create(&t2,NULL,threadfunc2,&loop);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
    printf("%d",glob);
}
void *threadfunc1(void *args){
  int loop,loc;
        loop=*(int*)args;
        for(int i=0;i<2000;i++){
                loc=glob;
                loc++;
                glob=loc;
        }

}
void *threadfunc2(void *args){
        int loop,loc;
        loop=*(int *)args;
        for(int i=0;i<2000;i++){
                loc=glob;
                loc++;
                glob=loc;
        }
output
4000
```
## Write a C program to create a thread that prints "Hello, World!"?
```
#include <stdio.h>
#include <pthread.h>
void *threadfun(void *args){
 char *sptr;
 sptr=(char *)args;
 printf("%s",sptr);
}
int main(){
pthread_t ti;
pthread_create(&ti,NULL,threadfun,"HELLO");
pthread_join(ti,NULL);
}
```
