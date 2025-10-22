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
## 3.

