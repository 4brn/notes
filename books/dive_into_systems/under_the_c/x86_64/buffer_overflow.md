## Buffer overflow
- The C programming language is not memory safe. It allows accessing memory outside of the bounds of an array which can result in a segfault. A clever attack can *inject* code that intentionally *overruns the boundary* of an array (also known as a **buffer**) to force a program to act in an unintended way. A piece of software that *exploits* such flaw is known as a **buffer overflow exploit**
## Famous Buffer Overflows
- while modern programs have protection against *overflows*, careless programming still leaves a lot of # opportunities.

#### Notable examples
- The Morris Worm
	- *worm* - harmless intellectual exercise
- AOL Chat Wars 
	- AOL started using a buffer overflow error _in their own client_ to verify that sent messages came from AIM clients. Since Microsoft’s Messenger Service (MMS) clients did not have the same vulnerability, the chat wars ended, with AOL as the victor.
- *reverse engineering* assembly - examining assembly code to reveal knowledge of how it works
## Guess the number
#### Definition
- goal is to win the game (get a return of 0).
- the game is asking for a secret number as well as a secret word.
- the program uses a potential vulnerability - `scanf` 
#### Information Gathering
- set a breakpoint just before the call to `fgets`
- before the call, the arguments are prepared (`%rax` & `%edi`)
	- the strings at the addresses can be examined by `x\s <address>`
![[Pasted image 20221120154716.png]]
- frame pointer `%ebp` is 32 bytes (`sub 0x20, %rsp`, `0x20` is 32 in decimal) away from stack pointer `%esp`
##### IMPORTANT (?)
- `x /48bx $rsp` -> inspect the 48 bytes below register `%rsp`
	- **!** `sub 0x20, %rsp` -> increase stack by 32 bytes
	- 8 bytes for saved `%rbp`
	- 8 bytes for *return address*
	- resulting in total of *48* bytes of stack.

##### IMPORTANT
![[Pasted image 20221120155910.png]]
1. the **byte** at address `0xf7ffffffdd00` is `0xf0`
2. the **byte** at address `0xf7ffffffdd01` is `0xdd`
3. the **byte** at address `0xf7ffffffdd02` is `0xff`
4. the **byte** at address `0xf7ffffffdd03` is `0xff`
5. the **byte** at address `0xf7ffffffdd04` is `0xff`
6. the **byte** at address `0xf7ffffffdd05` is `0x7f`
7. the **byte** at address `0xf7ffffffdd06` is `0x00`
8. the **byte** at address `0xf7ffffffdd07` is `0x00`
> the 64-bit VALUE AT ADDRESS 0x7fffffffdd00 is 0x7fffffffddf0
> this is because x86-64 is [little-endian](https://diveintosystems.org/book/C4-Binary/byte_order.html#_integer_byte_order)
- `buf` is located at the TOP of the stack and the first 2 addresses hold the inputted bytes associated with the input `123456789` + `\0` (a null byte)
- `0x00` is the null byte which terminates the string
- *!* `echo $?` prints the return value of the last executed command
#### Exploit 1
- if we run the program with a large string `1234567890123456789012345678901234567890123` the program crashes with a segmentation fault with return code `139`
- the input is so large that it *overflows* and *overwrites* the contents of `0xd08` (`x`) and `0xd10` (`saved %rbp`) but also the *return address* (`0xd18`)
	- *!* when the program returns, it tries to *resume execution* at the address *specified by the return address*
	- with input `1234567890`
	 ![[Pasted image 20221120161200.png]]
	- with input `1234567890123456789012345678901234567890123`
	![[Pasted image 20221120161222.png]]
		- **smashing the stack** -> the input created a *buffer overrun* and corrupted the stack causing a crash.
#### Exploit 2
- overwrite the stack so the *return address* is replaced with the address of `endGame`.
- to find the address of `endGame` use `disas endGame` (`0x00000000004006da`)
- craft a script which will fill in junk data and then a write the *new* return address.
```c
#include <stdio.h>

char ebuff[]=
"\x31\x32\x33\x34\x35\x36\x37\x38\x39\x30" /*first 10 bytes of junk*/
"\x31\x32\x33\x34\x35\x36\x37\x38\x39\x30" /*next 10 bytes of junk*/
"\x31\x32\x33\x34\x35\x36\x37\x38\x39\x30" /*following 10 bytes of junk*/
"\x31\x32\x33\x34\x35\x36\x37\x38\x39\x30" /*last 10 bytes of junk*/
"\xda\x06\x40\x00\x00\x00\x00\x00" /*address of endGame (little endian)*/
;

int main(void) {
    for (int i = 0; i < sizeof(ebuff); i++) printf("%c", ebuff[i]);
    return 0;
}
```
- compile the exploit, get the output -> `./secret < exploit.txt`
- `echo $?` returns 1!

## Protection
- *!* Old computer execute bytes from the stack memory. If bytes associated with assembly instructions are placed onto the stack CPU will execute them
- *Stack randomization*
	- randomize the starting position of the stack, multiple machines running the same code will have different stack addresses.
	- bypass -> use a **NOP sled** (i.e., a large number of `nop` instructions) before the actual exploit code.[Smashing the Stack for Fun and Profit](http://insecure.org/stf/smashstack.html). 1996. #look_into 
- *Stack corruption detection* 
	- use a *canary* which is a value stored in nonwriteable section of memory that can be compared to a value put on the stack. If canary "dies" program crashes.
	- bypass -> replace the canary to prevent detection
- *Limiting executable regions*
	- executable code is restricted to particular regions of memory.
	- bypass -> *return-oriented programming (ROP)*, "cherry-pick" instructions and jump from instruction to instruction to build an exploit.
- best line of defense is a good programmer and good code.

|Instead of: |Use:
--- | --- |
|gets(buf)|fgets(buf, 12, stdin)|
|scanf("%s", buf)|scanf("%12s", buf)|
|strcpy(buf2, buf)|strncpy(buf2, buf, 12)|
|strcat(buf2, buf)|strncat(bu2, buf, 12)|
|sprintf(buf, "%d", num)|snprintf(buf, 12, "%d", num)|
- `sprintf` -> store result string in buffer and not `stdout`
