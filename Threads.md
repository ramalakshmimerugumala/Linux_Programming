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
## 11.Write a C program to create a thread that prints "Hello, World!" with thread synchronization
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
void *myfunc(void *args){
        pthread_mutex_lock(&lock);
        printf("Hello World..");
        pthread_mutex_unlock(&lock);
}
int main(){
        pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,myfunc,NULL);
        pthread_join(t1,NULL);
        pthread_mutex_destroy(&lock);
}
```
## 12.Develop a C program to create two threads that print their thread IDs and synchronize their output
```
#include <pthread.h>
pthread_mutex_t lock;
void *func(void *args){
pthread_mutex_lock(&lock);
printf("%lu ",pthread_self());
pthread_mutex_unlock(&lock);
return NULL;
}
int main(){
        pthread_t t1,t2;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,func,NULL);
        pthread_create(&t2,NULL,func,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
        pthread_mutex_destroy(&lock);
}
```
## 13.Implement a C program to create a thread that generates random numbers and synchronizes access to a shared buffer?
```
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#define size 5
int buff[size];
int idx=0;
pthread_mutex_t lock;
void *myfunc(void *args){
      while(idx<size){
 pthread_mutex_lock(&lock);
      int num=rand()%100;
      buff[idx++]=num;
 pthread_mutex_unlock(&lock);
        }
 return NULL;
}
int main(){
 pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,myfunc,NULL);
        pthread_join(t1,NULL);
       pthread_mutex_destroy(&lock);
       for(int i=0;i<size;i++){
               printf("%d ",buff[i]);
       }
}
```
## 14 Write a C program to create a thread that performs addition of two numbers with mutex locks?
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
void *myfunc(void *args){
int *num=(int *)args;
int a=num[0];
int b=num[1];
 pthread_mutex_lock(&lock);
 printf("%d",a+b);
 pthread_mutex_unlock(&lock);
}
int main(){
pthread_t t1;
int num[2];
printf("Enter a number.");
scanf("%d",&num[0]);
printf("Enter a number");
scanf("%d",&num[1]);
pthread_mutex_init(&lock,NULL);
pthread_create(&t1,NULL,myfunc,&num);
pthread_join(t1,NULL);
pthread_mutex_destroy(&lock);
}
```
## 15 Implement a C program to create two threads that increment and decrement a shared variable, respectively, using mutex locks?
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
int sharedvar=0;
void *increment(void *args){
pthread_mutex_lock(&lock);
sharedvar++;
printf("Increment value=%d\n",sharedvar);
pthread_mutex_unlock(&lock);
}
void *decrement(void *args){
 pthread_mutex_lock(&lock);
 sharedvar--;
 printf("Decremented value=%d\n",sharedvar);
 pthread_mutex_unlock(&lock);
}
int main(){
 pthread_t t1,t2;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,increment,NULL);
        pthread_create(&t2,NULL,decrement,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
        pthread_mutex_destroy(&lock);
}
```
## 16 Develop a C program to create a thread that reads input from the user and synchronizes access to shared resources?
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
void *myfunc(void *args){
char sptr[100];
pthread_mutex_lock(&lock);
printf("Enter a string");
scanf("%s",sptr);
printf("you entered string=%s",sptr);
pthread_mutex_unlock(&lock);
}
int main(){
pthread_t t1;
pthread_mutex_init(&lock,NULL);
pthread_create(&t1,NULL,myfunc,NULL);
pthread_join(t1,NULL);
pthread_mutex_destroy(&lock);
}
```
## 17.Implement a C program to create a thread that prints prime numbers up to a given limit  with mutex locks?
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
int limit;
int prime(int n){
 for(int i=2;i*i<=n;i++){
         if(n%i==0){
                 return 0;
         }
 }
 return 1;
}
void *myfunc(void *args){
 pthread_mutex_lock(&lock);
 for(int i=2;i<=limit;i++){
         if(prime(i)){
            printf("%d ",i);
 }
 }
 pthread_mutex_unlock(&lock);
}
int main(){
pthread_t t1;
pthread_mutex_init(&lock,NULL);
printf("Enter limit");
scanf("%d",&limit);
pthread_create(&t1,NULL,myfunc,NULL);
pthread_join(t1,NULL);
pthread_mutex_destroy(&lock);
}
```
## 18 .Implement a C program to create a thread that calculates the sum of Fibonacci numbers up to a given limit using dynamic programming with mutex locks.
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
int limit;
void *myfunc(void *args){
        pthread_mutex_lock(&lock);
        int num1=0;
        int num2=1;
        printf("%d %d",num1,num2);
        int num3;
        int sum=num1+num2;
        for(int i=3;i<=limit;i++){
         num3=num1+num2;
         printf("%d ",num3);
         sum+=num3;
         num1=num2;
         num2=num3;
  }
        printf("%d",sum);
        pthread_mutex_unlock(&lock);
}
int main(){
        pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        printf("Enter a limit...");
        scanf("%d",&limit);
        pthread_create(&t1,NULL,myfunc,NULL);
        pthread_join(t1,NULL);
        pthread_mutex_destroy(&lock);
}
output
Enter a limit...10
0 1 1 2 3 5 8 13 21 34 88
```
## 19 .Write a C program to create a thread that checks if a given year is a leap year using dynamic programming with mutex locks
```
#include <stdio.h>
#include <pthread.h>
pthread_mutex_t lock;
void *myfunc(void *args){
int year=*(int*)args;
pthread_mutex_lock(&lock);
if(year%4==0 && year%100!=0 ||year%400==0){
        printf("Leap year");
}
else{
        printf("Not a leap year");
}
pthread_mutex_unlock(&lock);
return NULL;
}
int main(){
 pthread_t t1;
 int year;
 printf("Enter year");
 scanf("%d",&year);
 pthread_mutex_init(&lock,NULL);
 pthread_create(&t1,NULL,myfunc,&year);
 pthread_join(t1,NULL);
 pthread_mutex_destroy(&lock);
}
```
## 20.Write a C program to create a thread that checks if a given string is a palindrome using dynamic programming with mutex locks?
```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
pthread_mutex_t lock;
void *myfun(void *args){
char *str=(char *)args;
int len=strlen(str);
int pal=1;
pthread_mutex_lock(&lock);
for(int i=0,j=len-1;i<j;i++,j--){
if(str[i]!=str[j]){
        pal=0;
        break;
}
}
if(pal==1){
        printf("Palindrome");
` printf("Palindrome");
}
else{
printf("Not palindrome");
}
pthread_mutex_unlock(&lock);
}
int main(){
 char str[100];
 printf("Enter string.");
 scanf("%s",str);
 pthread_t t1;
 pthread_mutex_init(&lock,NULL);
 pthread_create(&t1,NULL,myfun,&str);
 pthread_join(t1,NULL);
 pthread_mutex_destroy(&lock);
}
```
## 21.



