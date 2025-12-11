### PIPE
```
#include <stdio.h>
#include <unistd.h>
#include <string.h>
int main(){
 int fd[2];
 pipe(fd);
 char buf[20];
 char buff[20];
 int id=fork();
 if(id==0){
        printf("child process..\n");
        close(fd[1]);
        read(fd[0],buf,sizeof(buf));
        printf(" Child Reading buf=%s",buf);
        close(fd[0]);
}
else{
   printf("Parent process..\n");
   printf("ENter a string.\n");
   scanf("%s",buff);
   close(fd[0]);
   write(fd[1],buff,strlen(buff));
   close(fd[1]);
}
}
```
## Named pipes
server
```
#include <sys/ipc.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
void main(){
char buf[60];
int fd;
int ret;
printf("Waiting for client to connect\n");
fd=open("fifoobj",O_RDONLY);
if(fd<0){
if((ret=mkfifo("fifoobj",0666))<0)
{
        printf("Error in creating fifo object.\n");
        return ;
}
fd=open("fifoobj",O_RDONLY);
}
printf("Client connected\n");
printf("Waiting for clinets message\n");
read(fd,buf,60);
printf("Message received :%s\n",buf);
}
```
client
```
#include <stdio.h>
#include <sys/ipc.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <string.h>
void main(){
 char buf[60];
 int fd;
 int ret;
 fd=open("fifoobj",O_WRONLY);
 if(fd<0){
  printf("Failed to open the file..");
 }
 printf("Enter the message for server\n");
 scanf("%s",buf);
 write(fd,buf,strlen(buf));
 printf("Message sent");
}
```
## message queues
srv
```
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/wait.h>
#include <sys/msg.h>
#define KEY 16548
#define SRV_MSG_TYPE 1
void main(){
        int msqid;
        char rxbuf[50];
msqid=msgget(KEY,0666|IPC_CREAT);
printf("Waiting for message from client\n");
msgrcv(msqid,rxbuf,50,SRV_MSG_TYPE,0);
printf("Message received from the client.%s\n",rxbuf+16);
}
```
client
```
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/wait.h>
#include <sys/msg.h>
#include <string.h>
#define KEY 16548
#define SRV_MSG_TYPE 1
void main(){
   int msqid;
   char txbuf[50];
msqid=msgget(KEY,0);
long int *ptr=(long*)(txbuf);
ptr[0]=SRV_MSG_TYPE;
scanf("%s",txbuf+16);
msgsnd(msqid,txbuf,8+8+strlen(txbuf+16),0);
printf("Message sent");
}
```

1 ## Create a program where two processes communicate synchronously using pipes. Ensure that one process waits for the other to finish before proceeding.
```
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <string.h>
#include <sys/wait.h>
int main(){
 int fd[2];
 int fds[2];
 pipe(fd);
 pipe(fds);
 char buf[40];
// char buff[50];
int id=fork();
if(id<0){
 printf("Error in creatinf fork");
}
if(id==0){
  printf("child process..\n");
  close(fd[1]);
  close(fds[0]);
  int n=read(fd[0],buf,sizeof(buf));
  printf("Child reading from parent %s\n",buf);
  write(fds[1],buf,strlen(buf));
  close(fd[0]);
  close(fds[1]);
}
else {
 printf("Parent process\n");
 close(fd[0]);
 close(fds[1]);
 printf("Enter a string..\n");
 scanf("%s",buf);
 write(fd[1],buf,strlen(buf));
 read(fds[0],buf,sizeof(buf));
 printf("parent received ack from child %s\n",buf);
 close(fd[1]);
 close(fds[0]);
wait(NULL);
}
}
```
## 2 Named pipes both server and receivr get  communicated and client getting acknowledgement from client
**Server Program**
```
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <string.h>
int main(){
char buf[50];
int ret;
int fd;
int fd2;
fd=open("fifobj",O_RDONLY);
if(fd<0){
 if ((ret=mkfifo("fifobj",0666|IPC_CREAT))<0){
         printf("Error in creating file..");
}
fd=open("fifobj",O_RDONLY);
}
printf("Server is waiting for client message..\n");
read(fd,buf,sizeof(buf));
printf("Message received from client %s\n",buf);
fd2=open("fifoobj",O_WRONLY);
if(fd2<0){
if(ret=(mkfifo("fifoobj",0670|IPC_CREAT))<0){
        printf("Error in opening the file.");
}
fd2=open("fifoobj",O_WRONLY);
}
char buff[20]="received";
write(fd2,buff,strlen(buff));
//printf("Message giving back to client %s\n",buff);
}
```
**Clinet Program**
```
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
int main(){
char buf[50];
int fd;
fd=open("fifobj",O_WRONLY);
printf(" Enter Client messgae..");
scanf("%s",buf);
write(fd,buf,strlen(buf));
printf("Message sent..\n");
int fd2=open("fifoobj",O_RDONLY);
printf("Client getting acknowledge from server\n");
read(fd2,buf,sizeof(buf));
printf("Acknowledgement from server %s\n",buf);
}
```

## 3. PIPES Toggle data send back from server
```
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <string.h>
#include <sys/wait.h>
int main(){
 int fd[2];
 int fds[2];
 pipe(fd);
 pipe(fds);
 char buf[40];
// char buff[50];
int id=fork();
if(id<0){
 printf("Error in creatinf fork");
}
void toggle(char *str){
        for(int i=0;str[i]!='\0';i++){
                if(str[i]>='a' && str[i]<='z')
                        str[i]=str[i]-32;
                else if(str[i]>='A' && str[i]<='Z')
                        str[i]=str[i]+32;
        }
           }
if(id==0){
  printf("child process..\n");
  close(fd[1]);
  close(fds[0]);
  int n=read(fd[0],buf,sizeof(buf));
  printf("Child reading from parent %s\n",buf);
  toggle(buf);
  write(fds[1],buf,strlen(buf)+1);
  close(fd[0]);
  close(fds[1]);
}
else {
 printf("Parent process\n");
 close(fd[0]);
 close(fds[1]);
 printf("Enter a string..\n");
 scanf("%s",buf);
 write(fd[1],buf,strlen(buf)+1);
read(fds[0],buf,sizeof(buf));
 printf("parent received ack from child %s\n",buf);
 close(fd[1]);
 close(fds[0]);
 wait(NULL);
}
}
 output
Parent process
Enter a string..
child process..
girl
Child reading from parent girl
parent received ack from child GIRL
```



