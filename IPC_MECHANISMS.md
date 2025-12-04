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
