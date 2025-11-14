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
## 1.Write a C program to create a thread that prints "Hello, World!"?
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
## 2.Modify the above program to create multiple threads, each printing its own message?
```
#include <stdio.h>
#include <pthread.h>
void *threadfunc1(void *args){
    char *ptr;
    ptr=(char *)args;
    printf("%s",args);
    printf("\n");
    return NULL;
}
int main(){
    pthread_t t1;
    pthread_t t2;
    pthread_create(&t1,NULL,threadfunc1,"Thread 1 says Hello");
    pthread_create(&t2,NULL,threadfunc1,"Thread 2 says World");
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
}
output
Thread 1 says Hello
Thread 2 says World
```
## 3 Develop a C program to create two threads that print numbers from 1 to 10 concurrently
```
#include <stdio.h>
#include <pthread.h>
void *threadfun(void *args){
    int id=*(int*)args;
  for(int i=1;i<=10;i++){
      printf("Threads %d =%d\n",id,i);
  }
  return NULL;
}
int main(){
    pthread_t t1,t2;
    int id=1;
    int id2=2;
    pthread_create(&t1,NULL,threadfun,&id);
    pthread_create(&t2,NULL,threadfun,&id2);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
}
```
## 4.Implement a C program to create a thread that calculates the factorial of a given number?
```
#include <stdio.h>
#include <pthread.h>
void *func(void *args){
    int fact=1;
    int num=*(int *)args;
  for(int i=1;i<=num;i++){
      fact=fact*i;
  }
  printf("%d",fact);
  return NULL;
}
int main(){
    int num;
    printf("ENter a number");
    scanf("%d",&num);
    pthread_t t1;
    pthread_create(&t1,NULL,func,&num);
    pthread_join(t1,NULL);
}
```
## 5.Write a C program to create two threads that print their thread IDs?
```
#include <stdio.h>
#include <pthread.h>
void *fun(void *args){
    int id=*(int *)args;
    printf("Threads%d=%lu ",id,pthread_self());
    return NULL;
}
int main(){
 pthread_t t1,t2;
 int id1=1;
 int id2=2;
 pthread_create(&t1,NULL,fun,&id1);
 pthread_create(&t2,NULL,fun,&id2);
 pthread_join(t1,NULL);
 pthread_join(t2,NULL);
}
output
Threads2=133309097727680 Threads1=133309106120384
```
## 6.Develop a C program to create a thread that prints the sum of two numbers
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
    int *number=(int *)args;
    int a=number[0];
    int b=number[1];
    printf("Sum of two numbers %d",a+b);
    return NULL;
}
int main(){
 pthread_t t1;
 int numbers[2];
 printf("Enter num1");
 scanf("%d",&numbers[0]);
 printf("enter number2");
 scanf("%d",&numbers[1]);
 pthread_create(&t1,NULL,myfunc,numbers);
 pthread_join(t1,NULL);
}
```
## 7..Implement a C program to create a thread that calculates the square of a number
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
    int num=*(int *)args;
    printf("%d",num*num);
    return NULL;
}
int main(){
    pthread_t t1;
    int num;
    printf("Enter a number");
    scanf("%d",&num);
    pthread_create(&t1,NULL,myfunc,&num);
    pthread_join(t1,NULL);
}
```
## 8..Write a C program to create a thread that prints the current date and time?
```
#include <stdio.h>
#include <pthread.h>
#include <time.h>
void *myfun(void *args){
   time_t t1;
   time(&t1);
   printf("Time and date=%s" ,ctime(&t1));
}
int main(){
    pthread_t t1;
    pthread_create(&t1,NULL,myfun,NULL);
    pthread_join(t1,NULL);
}
```
## 9.Develop a C program to create a thread that checks if a number is prime?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
    int num=*(int *)args;
    int flag=0;
    for(int i=2;i*i<=num;i++){
        if(num%i==0){
            flag=1;
        }
    }
    if(flag==1){
        printf("Not Prime");
        return 0;
    }
    printf("Prime number");
    return NULL;
}
int main(){
    pthread_t t1;
    int num;
    printf("Enter a number");
    scanf("%d",&num);
    pthread_create(&t1,NULL,myfunc,&num);
    pthread_join(t1,NULL);
}
```
## 10.Implement a C program to create a thread that checks if a given string is a palindrome
```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
void *myfun(void *args){
   char *sptr=(char*)args;
   int len=strlen(sptr);
     int flag=0;
   for(int i=0,j=len-1;i<j;i++,j--){
      if(sptr[i]!=sptr[j]){
         flag=1;
      }
   }
   if(flag==1){
       printf("String is not palindrome");
   }
   else{
       printf("Palindrome");
   }
   return NULL;
}
int main(){
 pthread_t t1;
 char str[100];
 printf("Enter a string");
 scanf("%s",str);
 pthread_create(&t1,NULL,myfun,&str);
 pthread_join(t1,NULL);
}
```
## 11.
