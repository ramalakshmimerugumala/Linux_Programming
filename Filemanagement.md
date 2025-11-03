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
## 1.Write a C program to create a new text file and write "Hello, World!" to it?
```
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <string.h>
#include <unistd.h>
int main(){
int fd;
if(fd<0){
        perror("Failure of opening the file..");
}
char buf[20]="HELLO WORLD!";
fd=open("demo.txt",O_WRONLY|O_CREAT,0640);
write(fd,buf,strlen(buf));
close(fd);
printf("Written Successfully..");
}
```
## 2.Develop a C program to open an existing text file and display its contents?
```
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
int main(){
int fd;
int n;
char buf[100];
if(fd<0){
        perror("Error in opening file..\n");
}
fd=open("demo.txt",O_RDONLY);
while((n=read(fd,buf,100))>0){
        printf("%s",buf);
}
close(fd);
}
```
## 3.Implement a C program to create a new directory named "Test" in the current directory?
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
int main(){
 int status;
 status=mkdir("Test",0650);
 if(status==0){
         printf("Created successfully");
 }
 else{
         perror("Failure");
 }
}
```
## 4.Write a C program to check if a file named "sample.txt" exists in the current directory?
```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <fcntl.h>
int main(){
   if(access("sample.txt",F_OK)==0){
           printf("sample.txt is present in the current directory..");
   }
   else{
      printf("It is not present in current directory.");
   }
}
```
## 5.Develop a C program to rename a file from "oldname.txt" to "newname.txt"?
```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
int main(){
int status;
int fd;
fd=open("old.txt",O_CREAT,0640);
status=rename("old.txt","new.txt");
if(status==0){
        printf("File name changed");
}
else{
   perror("Error in replacing");
}
}
```
## 6. Implement a C program to delete a file named "delete_me.txt"?
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(){
 int sta;
  sta=remove("del.txt");
  if(sta==0){
          printf("Deleted Succesfully");
  }
  else{
          perror("Deleting file");
  }
}
```
## 7. Develop a C program to move a file from one directory to another?
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(){
system("mv /home/ramalakshmi/linux/filemanagement/changedirectory.c /home/ramalakshmi/linux/processmanagement");
return 0;
}
```
## 8.

