## 1.Write System call
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
int main(){
int fd,x;
char buf[10];
printf("Enter a  string");
scanf("%s",buf);
fd=open("file.txt",O_WRONLY);
if(fd<0){
        printf("Couldn't open the file");
        exit(1);
}
write(fd,buf,strlen(buf));
close(fd);
return 0;
}
```
## 2.Truncate
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
int main(){
int fd,x;
char buf[10];
printf("Enter a  string");
scanf("%s",buf);
fd=open("file.txt",O_WRONLY|O_TRUNC);
if(fd<0){
        printf("Couldn't open the file");
        exit(1);
}
write(fd,buf,strlen(buf));
close(fd);
return 0;
}
```
## 3.Copy
```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
int main(){
char buf[100];
int srcfd,destfd;
int number;
srcfd=open("file.txt",O_RDONLY);
destfd=open("file2.txt",O_WRONLY|O_CREAT,0640);
while((number=read(srcfd,buf,100))>0){
                write(destfd,buf,number);
}
}
```
## 4. Copying one file to another by using command line argument
```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
int main(int argc,char *argv[]){
        char buf[100];
        int srcfd,destfd,number;
 srcfd=open(argv[1],O_RDONLY);
 destfd=open(argv[2],O_WRONLY);
 while((number=read(srcfd,buf,100))>0){
         write(destfd,buf,number);
 }
}
```
## 5.Printing the size of the file
```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>
int main(){
 int fd;
 struct stat buf;
 fd=open("file.txt",O_RDWR);
 fstat(fd,&buf);
 printf("%ld",buf.st_size);
 close(fd);
}
```
## 6.

