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
## 21.Implement a C program to create a thread that performs selection sort on an array of integers?
```
#include <stdio.h>
#include <pthread.h>
void *func(void *args){
 int *arr=(int*)args;
 int n=5;
 for(int i=0;i<5;i++){
         int min=i;
         for(int j=i+1;j<n;j++){
                 if(arr[j]<arr[min]){
                         min=j;
                 }
         }
         int temp=arr[i];
         arr[i]=arr[min];
         arr[min]=temp;
 }
 return NULL;
}
int main(){
pthread_t t1;
int arr[5];
printf("Enter elements in the array");
for(int i=0;i<5;i++){
        scanf("%d",&arr[i]);
}
pthread_create(&t1,NULL,func,&arr);
pthread_join(t1,NULL);
for(int i=0;i<5;i++){
        printf("%d",arr[i]);
}
}
```
## 22..Develop a C program to create a thread that calculates the area of a triangle?
```
#include <stdio.h>
#include <pthread.h>
void *area(void *args){
        float *arr=(float *)args;
        float base=arr[0];
        float height=arr[1];
        float area=0.5*base*height;
        printf("Area=%f",area);
        return NULL;
}
int main(){
pthread_t t1;
float arr[2];
printf("Enter base value");
scanf("%f",&arr[0]);
printf("Enter Height value");
scanf("%f",&arr[1]);
pthread_create(&t1,NULL,area,arr);
pthread_join(t1,NULL);
}
```
## 23.Write a C program to create a thread that calculates the sum of squares of numbers from 1 to 100?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
 int sum=0;
 for(int i=1;i<=100;i++){
   sum+=i*i;
}
printf("%d",sum);
return NULL;
}
int main(){
 pthread_t t1;
 pthread_create(&t1,NULL,myfunc,NULL);
 pthread_join(t1,NULL);
}
```
## 24.Write a C program to create a thread that generates a random array of integers?
```
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#define size 5
int arr[size];
void *myfunc(void *args){
 for(int i=0;i<5;i++){
   arr[i]=rand()%100;
 }
 return NULL;
}
int main(){
pthread_t t1;
srand(time(NULL));
pthread_create(&t1,NULL,myfunc,&arr);
pthread_join(t1,NULL);
for(int i=0;i<5;i++){
   printf("%d ",arr[i]);
}
}
```
## 25 Implement a C program to create a thread that performs bubble sort on an array of integers?
```
#include <stdio.h>
#include <pthread.h>
#define size 5
void *bubble(void *args){
  int *arr=(int *)args;
  for(int i=0;i<size;i++){
          for(int j=0;j<size-i-1;j++){
                  if(arr[j]>arr[j+1]){
                      int temp=arr[j];
                      arr[j]=arr[j+1];
                      arr[j+1]=temp;
                  }
          }
  }
  return NULL;
}
int main(){
int arr[5];
        pthread_t t1;
        printf("Enter the elements in the array");
        for(int i=0;i<5;i++){
             scanf("%d",&arr[i]);
        }
        pthread_create(&t1,NULL,bubble,&arr);
        pthread_join(t1,NULL);
        for(int i=0;i<5;i++){
                printf("%d ",arr[i]);
        }
}
```
## 26 .Develop a C program to create a thread that calculates the greatest common divisor (GCD) of two numbers?
```
#include <stdio.h>
#include <pthread.h>
void *gcd(void *args){
        int *num=(int *)args;
        int a=num[0];
        int b=num[1];
        int min;
        min=(a<b)?a:b;
        while(1){
   if(a%min==0 && b%min==0){
  printf("GCD of two numbers=%d",min);
   break;
   }
   min--;
}
return NULL;
}
int main(){
pthread_t t1;
int num[2];
printf("Enter a number1");
scanf("%d",&num[0]);
printf("Enter number2");
scanf("%d",&num[1]);
pthread_create(&t1,NULL,gcd,&num);
pthread_join(t1,NULL);
}
```
## 27.Implement a C program to create a thread that calculates the sum of even numbers from 1to 100?
```
#include <stdio.h>
#include <pthread.h>
void *even(void *args){
int sum=0;
for(int i=0;i<=100;i++){
        if(i%2==0){
                sum+=i;
}
}
printf("%d",sum);
return NULL;
}
int main(){
 pthread_t t1;
 pthread_create(&t1,NULL,even,NULL);
 pthread_join(t1,NULL);
}
```
## 28.Implement a C program to create a thread that performs multiplication of two matrices?
```
#include <stdio.h>
#include <pthread.h>
int arr1[3][2];
int arr2[2][3];
int arr3[100][100];
void *matrix(void *args){
        for(int i=0;i<3;i++){
                for(int j=0;j<3;j++){
                        arr3[i][j]=0;
                }
        }
 for(int i=0;i<3;i++){
         for(int j=0;j<3;j++){
                 for(int k=0;k<2;k++){
                        arr3[i][j]+=arr1[i][k]*arr2[k][j];
                 }
         }
 }
 return NULL;
}
int main(){
pthread_t t1,t2;
printf("Enter the elemets in the first array");
for(int i=0;i<3;i++){
        for(int j=0;j<2;j++){
                scanf("%d",&arr1[i][j]);
        }
}
printf("Enter the elements in the array2");
for(int i=0;i<2;i++){
for(int j=0;j<3;j++){
                scanf("%d",&arr2[i][j]);
        }
}
pthread_create(&t1,NULL,matrix,NULL);
pthread_join(t1,NULL);
printf("Resultant matrix:");
for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
                printf("%d ",arr3[i][j]);
        }
        printf("\n");
}
}
```
## 29.Implement a C program to create a thread that generates a random string?
```
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
void *myfunc(void *args){
 char str[100];
 int length=*(int*)args;
 for(int i=0;i<length;i++){
         str[i]='A'+rand()%26;
 }
 str[length]='\0';
 printf("Random string=%s",str);
}
int main(){
 pthread_t t1;
 int len;
 printf("Enter a length");
 scanf("%d",&len);
srand(time(NULL));
 pthread_create(&t1,NULL,myfunc,&len);
 pthread_join(t1,NULL);
}
```
## 30.Develop a C program to create a thread that calculates the average of numbers from 1 to100?
```
#include <stdio.h>
#include <pthread.h>
void* calc_average(void* arg) {
    int sum = 0;
    for (int i = 1; i <= 100; i++) {
        sum += i;
    }
    float avg = sum / 100.0;
    printf("Average of numbers 1 to 100 = %.2f\n", avg);

    return NULL;
}
int main() {
    pthread_t t1;
    pthread_create(&t1, NULL, calc_average, NULL);
    pthread_join(t1, NULL);
    return 0;
}
```
## 31.Write a C program to create a thread that checks if a given number is a perfect square?
```
#include<stdio.h>
#include <pthread.h>
void *myfun(void *args){
    int num=*(int*)args;
    int flag=0;
    for(int i=1;i<=num;i++){
        if(i*i==num){
            flag=1;
        }
    }
    if(flag==1){
        printf("Perfect square");
    }
    else{
        printf("Not a perfect square");
    }
    return NULL;
}
int main(){
   pthread_t t1;
   int num;
   printf("Enter a number");
   scanf("%d",&num);
   pthread_create(&t1,NULL,myfun,&num);
   pthread_join(t1,NULL);
}
```
## 32 Implement a C program to create a thread that calculates the factorial of a given number using recursion?
```
#include <stdio.h>
#include <pthread.h>
int factorial(int n){
 if(n<=1)
 return 1;
 return n*factorial(n-1);
}
void *myfunc(void *args){
    int num=*(int*)args;
    int result=factorial(num);
    printf("Facorial of a number=%d",result);
}
int main(){
    int num;
    printf("Enter a number");
    scanf("%d",&num);
    pthread_t t1;
    pthread_create(&t1,NULL,myfunc,&num);
    pthread_join(t1,NULL);
}
```
## 33.Develop a C program to create a thread that finds the maximum element in an array
```
#include <stdio.h>
#include <pthread.h>
int arr[5];
void *myfunc(void *args){
    int max=arr[0];
    for(int i=0;i<5;i++){
        if(arr[i]>max){
            max=arr[i];
        }
    }
    printf("%d",max);
    return NULL;
}
int main(){
    printf("Enter the elements in the array");
    for(int i=0;i<5;i++){
        scanf("%d",&arr[i]);
    }
    pthread_t t1;
    pthread_create(&t1,NULL,myfunc,arr);
    pthread_join(t1,NULL);
}
```
## 34.Write a C program to create a thread that sorts an array of strings?
```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
char str[10][50];
char temp[50];
int n=5;
void *myfunc(void *args){
    for(int i=0;i<n;i++){
        for(int j=0;j<n-i-1;j++){
            if(strcmp(str[j],str[j+1])>0){
                strcpy(temp,str[j]);
                strcpy(str[j],str[j+1]);
                strcpy(str[j+1],temp);
            }
        }
    }
    return NULL;
}
int main(){
    printf("Enter strings");
    for(int i=0;i<n;i++){
        scanf("%s",str[i]);
    }
    pthread_t t1;
    pthread_create(&t1,NULL,myfunc,NULL);
    pthread_join(t1,NULL);
    printf("Sorted strings..");
    for(int i=0;i<n;i++){
        printf("%s\n",str[i]);
    }
}
```
## 35 Implement a C program to create a thread that calculates the square root of a number?
```
#include <stdio.h>
#include <pthread.h>
#include <math.h>

void* calculate_sqrt(void *args) {
    double num = *(double*)args;
    double result = sqrt(num);
    printf("Square root of %.2f = %.2f\n", num, result);
    return NULL;
}

int main() {
    pthread_t t1;
    double num;

    printf("Enter a number: ");
    scanf("%lf", &num);

    pthread_create(&t1, NULL, calculate_sqrt, &num);
    pthread_join(t1, NULL);

    return 0;
}
```
## 36 Write a C program to create a thread that generates a random password?
```
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
int len;
void *myfunc(){
    char charset[]="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890!@#$%^&";
    char password[len+1];
    for(int i=0;i<len;i++){
    int index=rand()%(sizeof(charset-1));
    password[i]=charset[index];
    }
    password[len]='\0';
    printf("Random password=%s",password);
    return NULL;
}
int main(){
    printf("Enter a length of a password");
    scanf("%d",&len);
pthread_t t1;
srand(time(NULL));
pthread_create(&t1,NULL,myfunc,NULL);
pthread_join(t1,NULL);
}
```
## 37 Write a C program to create a thread that calculates the factorial of numbers from 1 to 10?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
        int fact=1;
    for(int i=1;i<=10;i++){
            fact=fact*i;
    printf("Factorial of %d is %d\n",i,fact);
    }
}
int main(){
        pthread_t t1;
        pthread_create(&t1,NULL,myfunc,NULL);
        pthread_join(t1,NULL);
}
```
## 38.Write a C program to create two threads using pthreads library. Each thread should print "Hello, World!" along with its thread ID?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
 printf("Hello World..\n");
 printf("%lu\n",pthread_self());
}
void *myfunc2(void *args){
        printf("Hello World..\n");
        printf("%lu\n",pthread_self());
        return NULL;
}
int main(){
pthread_t t1,t2;
pthread_create(&t1,NULL,myfunc,NULL);
pthread_create(&t2,NULL,myfunc2,NULL);
pthread_join(t1,NULL);
pthread_join(t2,NULL);
}
```
## 39..Modify the previous program to pass arguments to the threads and print those arguments along with the thread ID?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
  int val=*(int*)args;
  printf("%d\n",val);
 printf("Hello World..\n");
 printf("%lu\n",pthread_self());
}
void *myfunc2(void *args){
        int val2=*(int*)args;
        printf("%d\n",val2);
        printf("Hello World..\n");
        printf("%lu\n",pthread_self());
        return NULL;
}
int main(){
pthread_t t1,t2;
int a1=10;
int a2=20;
pthread_create(&t1,NULL,myfunc,&a1);
pthread_create(&t2,NULL,myfunc2,&a2);
pthread_join(t1,NULL);
pthread_join(t2,NULL);
}
```
## 40Write a C program to demonstrate thread synchronization using mutex locks. Create two threads that increment a shared variable using mutex locks to ensure proper synchronization?
```
#include <stdio.h>
#include <pthread.h>
int shared_var=0;
pthread_mutex_t lock;
void *myfunc(void *args){
    pthread_mutex_lock(&lock);
    shared_var++;
    printf("Thread1=%d ",shared_var);
    pthread_mutex_unlock(&lock);
}
void *myfunc2(void *args){
    pthread_mutex_lock(&lock);
    shared_var++;
    printf("Thread2=%d ",shared_var);
    pthread_mutex_unlock(&lock);
}
int main(){
    pthread_t t1,t2;
    pthread_mutex_init(&lock,NULL);
    pthread_create(&t1,NULL,myfunc,NULL);
    pthread_create(&t2,NULL,myfunc2,NULL);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
    pthread_mutex_destroy(&lock);
}
```
## 41 Extend the previous program to use semaphore instead of mutex locks for thread synchronization?
```
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
int shared_var=0;
sem_t  sem;
void *myfunc(void *args){
    sem_wait(&sem);
    shared_var++;
    printf("Thread1=%d",shared_var);
    sem_post(&sem);
    return NULL;
}
void *myfunc2(void *args){
    sem_wait(&sem);
    shared_var++;
    printf("Thread2=%d",shared_var);
    sem_post(&sem);
    return NULL;
}
int main(){
    pthread_t t1,t2;
    sem_init(&sem,0,1);
    pthread_create(&t1,NULL,myfunc,NULL);
    pthread_create(&t2,NULL,myfunc2,NULL);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
    sem_destroy(&sem);
}
```
## 42.Write a C program to implement the producer-consumer problem using pthreads. Create two threads - one for producing items and another for consuming items from a shared buffer?
```
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
sem_t empty;
sem_t full;
int buffer[5];
void *producer(void *args){
    for(int i=1;i<5;i++){
        sem_wait(&empty);
        buffer[i]=i;
    printf("Producer Buffer=%d\n",buffer[i]);
    sem_post(&full);
    }
    return NULL;
}
void *consumer(void *args){
    
    for(int i=1;i<5;i++){
        sem_wait(&full); 
    printf("Consumer buffer=%d\n",buffer[i]);
    sem_post(&empty);
    }
    return NULL;
}
int main(){
    pthread_t t1,t2;
    sem_init(&empty,0,1);
    sem_init(&full,0,0);
    pthread_create(&t1,NULL,producer,NULL);
    pthread_create(&t2,NULL,consumer,NULL);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
    sem_destroy(&empty);
    sem_destroy(&full);
}
```
## 43 Write a C program to demonstrate thread cancellation. Create a thread that runs an infinite loop and cancels it after a certain condition is met from the main thread?
```
#include <stdio.h>
#include <pthread.h>
#include<unistd.h>
void *infiniteloop(void *args){
    while(1){
        printf("Infinite loop..\n");
        sleep(1);
    }
    return NULL;
}
int main(){
    pthread_t t1;
    pthread_create(&t1,NULL,infiniteloop,NULL);
    sleep(5);
    printf("Main:cancelling the infinite loop");
    pthread_cancel(t1);
    pthread_join(t1,NULL);
}
```
## 44 .Write a C program to create a thread that prints the even numbers between 1 and 20?
```
#include <stdio.h>
#include <pthread.h>
void *even(void *args){
    //int num=*(int *)args;
    for(int i=0;i<=20;i++){
    if(i%2==0){
        printf("Even=%d\n",i);
    }
    else{
        printf("Odd=%d\n",i);
    }
    }
    return NULL;
}
int main(){
    pthread_t t1,t2;
    pthread_create(&t1,NULL,even,NULL);
    pthread_create(&t2,NULL,even,NULL);
    pthread_join(t1,NULL);
    pthread_join(t2,NULL);
}
```
## 45 .Implement a C program to create a thread that calculates the sum of squares of numbers from 1 to 10?
```
#include <stdio.h>
#include <pthread.h>
void *myfunc(void *args){
 int sum=0;
 for(int i=0;i<=10;i++){
         sum+=i*i;
}
printf("%d",sum);

return NULL;
}
int main(){
        pthread_t t1;
        pthread_create(&t1,NULL,myfunc,NULL);
        pthread_join(t1,NULL);
}
```
## 46.Implement a C program to create a thread that prints the factors of a given number?
```
#include <stdio.h>
#include <pthread.h>
void *factors(void *args){
 int num=*(int*)args;
 for(int i=1;i<=num;i++){
     if(num%i==0){
             printf("factors=%d\n",i);
     }
}
return NULL;
}
int main(){
int num;
printf("ENter a number");
scanf("%d",&num);
pthread_t t1;
pthread_create(&t1,NULL,factors,&num);
pthread_join(t1,NULL);
}
```
## 47 Develop a C program to create a thread that prints the English alphabet in uppercase?
```
#include <stdio.h>
#include <pthread.h>
void *upper(void *args){
  for(char ch='A';ch<='Z';ch++){
          printf("%c",ch);
}
return NULL;
}
int main(){
pthread_t t1;
pthread_create(&t1,NULL,upper,NULL);
pthread_join(t1,NULL);
}
```
## 48 Implement a C program to create a thread that checks if a given number is divisible by another given number?
```
#include <pthread.h>
void *myfunc(void *args){
 int *num1=(int *)args;
 int a=num1[0];
 int b=num1[1];
 if(a%b==0){
         printf("%d is divisibel by %d",a,b);
}
else{
        printf("Not divisible");
}
return NULL;
}
int main(){
        int num[2];
        printf("ENter a number1");
        scanf("%d",&num[0]);
        printf("Enter number2");
        scanf("%d",&num[1]);
        pthread_t t1;
        pthread_create(&t1,NULL,myfunc,&num);
        pthread_join(t1,NULL);
}
```
## 49.


