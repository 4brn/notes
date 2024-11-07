## CTF
- This is my first attempt at creating a basic CTF

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(){
	char* name = (char*) malloc(sizeof(char) * 5);
	int* passcode = (int*) malloc(sizeof(int));
	
	srand(time(0));
	*passcode = (rand() % 1000);

	printf("Enter your username: ");
	scanf("%s", name);

	printf("Enter a passcode: ");
	int userInput;
	scanf("%d", &userInput);

	if(userInput == *passcode){
		printf("NOICE{876184762387462831}\n");
	}else{
		printf("Wrong passcode!\n");
	}
	
	free(name);
	free(passcode);	
}
```
- A username is wanted from the user and then the correct password which is generated randomly (with time as the seed if that's random).
- By providing `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` (34 `a` characters) as the username input the content to which `passcode` points gets changed to `97` (the ascii code of `a`).
- This is because `scanf` doesn't check for how big the input is and allows *buffers overflows*.

- If the variables were declared on the stack there would've been a *stack smashing*
	- 