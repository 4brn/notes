e# GNU Debugger (GDB)
- use `file {filename}` to get information about a file.

## 3.1 Debuggin with GDB
- GDB has all the features of a debugger (strp through program, break points, examine variables, etc)
- Data Display Debugger (*DDD*) - GUI wrapper for a command line debugger (e.g. GDB)
### 3.1.1 Gettign Started with GDB
- when debugging compile with the `-g` (or `-g3`) option as it adds additional information.
- don't use optimization flags such as `-O2`.
- use `gdb core a.out` to examine the contents of the dumped core (in case of such error)
	- `where` command shows point of crash

### 3.1.2 Example GDB Sessions

#### Commands

- *break* -> Set a breakpoint
- *run*   -> Start a program running from the beginning
- *cont*  -> Continue execution of the program until it hits a breakpoint
- *quit*  -> Quit the GDB session
- *next*  -> Allow program to execute the next line of C code and then pause it
- *step*  -> Allow program to execute the next line of C code; if the next line contains a function call, step into the function and pause
- *list*  -> List C source code around pause point or specified point
- *print* -> Print out the value of a program variable (or expression)
- *where* -> Print the call stack
- *frame* -> Move into the context of a specific stack frame

### Practise
#### Logical error
- set a break point at main - `break main`
- `run` (if arguments should be specified do `run arg1 arg2`)
- use `list {function name}` to list the code around a specific function
- to join function execution use `step` instead of `next` (the latter treats a function as one step)
- use `display {var_name}` to display this variable everytime a *breakpoint* is hit![[Pasted image 20221023131242.png]]
- `where` or `bt` to print the stack trace

#### Crash
- let the program *segfault* by typing `run`
- type `where` to see where was the *segmentation fault*
- `list` is also useful to show the code around the crash
- we can see that the problem is accessing memory out of scope
- by printing the value of `array` we can see that it's a *null pointer* and *dereferencing* a null pointer (`array[i]`) gives an error
![[Pasted image 20221023134605.png]]


## 3.2 GDB commands in detail

### 3.2.1 Keyboard Shortcuts in GDB
- shortcuts -> `l` for `list`, `p` for `print`, etc
- hit `RETURN` to run the last command
### 3.2.2 Common GDB Commands

#### Execution control flow
- *help* -> get the docs
- *break*
	```
	break <func-name>   Set breakpoint at start of function <func-name>
	break <line>        Set breakpoint at line number <line>
	break <filename:><line>  Set breakpoint at <line> in file <filename>
	
	break main          Set breakpoint at beginning of main
	break 13            Set breakpoint at line 13
	break gofish.c:34   Set breakpoint at line 34 in gofish.c
	break main.c:34     Set breakpoint at line 34 in main.
	```
- *run*
	```
	run <command line arguments>
	
	run             Run with no command line arguments
	run 2 40 100    Run with 3 command line arguments: 2, 40, 100
	```
- *continue* - continues to the next breakpoint
- *step* - executes the next line (goes into a function if there is one)
- *next* - executes the next line.
- *until* -> `until <line>` -> execute until the specified line number
- *quit* -> exit.

#### Examining and listing the program code
- *list* - list source code
```
	list                Lists next few lines of program source code
	list <line>         Lists lines around line number <line> of program
	list <func-name>    Lists lines around beginning of function <func-name>
```
- *where* (*backtrace* or *bt* ) -> shows the stack trace
- *frame* - move into the context of a specified stack frame (`frame <numer>`)
#### BREAKPOINTS
- *break* - set a breakpoint (start of a function or line)
- *enable*, *disable*, *ignore*, *delete*, *clear* 
	- "Enable, disable, ignore for some number of times, or delete one or more breakpoints. The `delete` command deletes a breakpoint by its number. In contrast, using the `clear` command deletes a breakpoint at a particular location in the source code"
- *condition* - stop on condition
	- `condition <bpnum> <exp>` (bpnum -> breakpoint number)
	- `condition 1 (i > 1000)`
#### STATE
- *print* - print value, supports different formats (`/x`, `/t`, etc)
	- `print $eax` -> print value stored in the eax register
- *display* - automatically display the value of an expression when breakpoint reached.
- *x* - examine memory
- *whatis* - show the type of an expression
- *set* - change the value of a a variable
- *info* - information about the program state


## 3.3 Debugging Memory with Valgrind
- highlights *heap memory* errors in programs (`malloc()` and `free()`)
- Common errors:
	- reading a value from uninitialized memory.
	- reading or writing at an unallocated memory location. Often indicates *array out-of-bounds* error.
	- freeing already free memory
	- memory leaks
		```c
		ptr = malloc(sizeof(int) * 10);
		ptr = malloc(sizeof(int) * 5);  // memory leak of first malloc of 10 ints
		```

#### INTERESTING

```c
 1  #include <stdio.h>
 2  #include <stdlib.h>
 3
 4  /* print size elms of array p with name name */
 5  void print_array(int *p, int size, char *name) ;
 6
 7  int main(int argc, char *argv[]) {
 8      int *bigfish, *littlefish, i;
 9
10      // allocate space for two int arrays
11      bigfish = (int *)malloc(sizeof(int) * 10);
12      littlefish = (int *)malloc(sizeof(int) * 10);
13      if (!bigfish || !littlefish) {
14          printf("Error: malloc failed\n");
15          exit(1);
16      }
17      for (i=0; i < 10; i++) {
18          bigfish[i] = 10 + i;
19          littlefish[i] = i;
20      }
21      print_array(bigfish,10, "bigfish");
22      print_array(littlefish,10, "littlefish");
23
24      // here is a heap memory access error
25      // (write beyond bounds of allocated memory):
26      for (i=0; i < 13; i++) {
27          bigfish[i] = 66 + i;
28      }
29      printf("\nafter loop:\n");
30      print_array(bigfish,10, "bigfish");
31      print_array(littlefish,10, "littlefish");
32
33      free(bigfish);
34      free(littlefish);  // program will crash here
35      return 0;
36  }
```
- there wil be a *heap memory access* error in the second for loop (line 26) 

- most likely reason for a crash is because by going over the limit of `bigfish` the *meta-data* of `littlefish` gets overwritten and then `free` doesn't know how much stuff to free [more](obsidian://open?vault=systems&file=deeper_dive%2Fdeeper_c%2Fvm-freespace)
![[Pasted image 20221023150210.png]]

- *Valgrind* comes into help in similar situations. (works only for heap memory errors)
```
Invalid write
 at main (bigfish.c:27)
 Address is 0 bytes after a block of size 40 alloc'd
   by main (bigfish.c:11)
```
- similar errors can happen with stack and global memory 
> overwriting memory locations beyond the bounds of a statically declared array on the stack may result in "mysteriously" changing the values of other local variables


- Read the part of the book talking about using valgrind [here](https://diveintosystems.org/book/C3-C_debug/valgrind.html#_how_to_use_memcheck)
- Valgrind's default tool is *memcheck*
- `--leak-check=yes` for memory leaks details
- Example of Valgrind's output
![[Pasted image 20221023153506.png]]
- says that the error is in `valgrindbadprog.c` at `foo` on line `29` (array out of bonds error in there)
## 3.4 Advanced GDB Features
> go through this chapter again once you've read the "Operating Systems" one.

### 3.4.1 GDB and make
- GDB accepts the *make* command to rebuild during debuggin.
	- useful as it allows to modify the code and keep the breakpoints
	- can mess up the breakpoints if code is added/removed
### 3.4.2 Attaching GDB to a Running Process
- get the *PID* (*Process ID*) 
- `ps -A | grep a.out`
- `gdb <executable> <pid>`
### 3.4.3 Following a Process on a Fork
- `fork()` function creates a new child process
	- `gdb` can follow either the main process or the child one.
	- by default it follows the main (parent) process
	- to change `(gdb) set follow-fork-mode <parent|child>`
### 3.4.4 Signal Control
- `gdb` can send signal to the process it debugs
	- `(gdb) signal SIGCONT`
	- `(gdb) signal SIGALARM`
### DDD Settings and Bug Fixes
- don't use `DDD`

## 3.5 Debugging Assembly Code

#for_later -> look into this section once you've completed the assembly part

## 3.6 Debugging Multi-threaded Programs
#for_later -> look into once you reach multi-threaded programs