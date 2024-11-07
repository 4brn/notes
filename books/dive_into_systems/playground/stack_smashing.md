[scanf()](https://www.youtube.com/watch?v=RAbwchpvO1s) a video covering most of the content in here.

```c
#include <stdio.h>
#include <stdlib.h>

int main(){
	char myinput[10];
	scanf("%s", myinput);
	printf("%s\n", myinput);

	return 0;
}
```
- if the snippet above is ran with input more than `10` it will cause *stack smashing*

```c
#include <stdio.h>
#include <stdlib.h>

int main(){
	char myinput[10];
	char str[10] = "hello";
	scanf("%s", myinput);
	printf("%s\n", myinput);
	printf("%s\n", str);
	return 0;
}
```
- in this case though, there will be no *stack smashing* as the additional characters will go into the `str` array.


## Buffer Overflow

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h> 

int main(){
	char myinput[10];
	char mypasswd[10] = "pass";
	scanf("%s", myinput);
	
	if(strcmp(myinput, mypasswd) == 0){
		printf("FLAG{123876342658}:\n");
	}else{
		printf("Wrong password\n");
	}
	printf("mypass -> %s\n", mypasswd);

	return 0;
}
```
- data on the stack is stored in sequence.
- `./a.out < <(python -c "print('aaaaaaaaa' + '\x00' + 'aaaaaaaaa' + '\x00')")` 
	- if we know that `myinput` and `mypasswd` have both length of 10 we can send 9`a` and a *null byte* (`\x00`) which is used to separate strings. Then mypasswd is filled with the same content. 

## Fix
- change `scanf("%s", myinput)` to `scanf("%10s", myinput)` which means that `scanf` will take only 10 bytes.
- Be very careful when using `scanf`.


## Stack smashing
- *stack smashing* is caused when one writes/over-allocates too much data in a given part of the stack, thereby overwriting another part of the stack. It is detected by *stack canaries*  or *canary bytes* which if overwritten raise an error. 
- If it is not enabled, buffer overflows can lead to chainging the `jmp` pointer and maybe running a shellcode.