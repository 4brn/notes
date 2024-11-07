# 2.9.5 C Libraries: Using, Compiling, and Linking (p.133)

#### Library 
> library implements a collection of functions and definitions that can be used by other programs
> different view can be gound [here](https://www.cs.swarthmore.edu/~newhall/unixhelp/compilecycle.html)


### A C library consists of:
1. The *application programming interface* (**API**)
	- gets defined in header files (`.h`) which must be included in source files that plan to use the library
	- include: function prototypes, type, constant or global variable declarations.
2. The *implementation* of the library's functionality
	- often available in a *precompiled binary* format that gets *linked* (added) into the binary executable created by gcc. Precompiled binary code can be:
		- *archive file* (`mylib.a`) containing several `.o` files that can be statically linked at compile time
		- *shared object file* (`mylib.so`) that can be dynamically linked at runtime
	- consists of >= 1 modules (`.c` files)
	- precompiled binaries cannot be ran but provide code that can be *linked* into an exe at compilation
	- can be linked with `-l`
		- `gcc -o myprog myprog.c -lpthread -lreadline` - links `pthread` and `readline`
		- `gcc -o myprog myprog.c --static -lpthread -lreadline` - static


### Compilation Steps
> Compilation (`main.c ---> a.out`) consists of 4 steps + 1 at runtime.

```c
// main.c

#define FAV_NUM 3	
int main()
{
	int a = 3 + FAV_NUM;
	return 0;
}
```
> will use the code above for all examples


1. *Precompiler* - expands *preprocessor directives* (`#define`, `#include`, etc)  
	- `gcc -E main.c`
	```c
	int main()
	{
		int a = 3 + 3;
		return 0;
	}
	```

2. *Compile* - translates source code (`main.c`) to assembly (`main.s`)
	- includes *compilation errors* such as: syntax errors, undefined symbol warnings, errors from missing definitions.
	- `gcc -S main.c`
	```asm
		.file	"main.c"
		.text
		.globl	main
		.type	main, @function
	main:
	.LFB0:
		.cfi_startproc
		pushq	%rbp
		.cfi_def_cfa_offset 16
		.cfi_offset 6, -16
		movq	%rsp, %rbp
		.cfi_def_cfa_register 6
		movl	$6, -4(%rbp)
		movl	$0, %eax
		popq	%rbp
		.cfi_def_cfa 7, 8
		ret
		.cfi_endproc
	.LFE0:
		.size	main, .-main
		.ident	"GCC: (GNU) 12.2.0"
		.section	.note.GNU-stack,"",@progbits
		
	```
3. *Assembly* -> converts assembly into *relocatable binary object code* (`main.o`) 
	- not a complete executable
	- *ELF* (Executable and Linkable Format)
	- `gcc -c main.c`
	- to view use `objdump -d main.o`
4. *Link editing* - creates a single executable file (`a.out`) from relocatable binaries (`.o`) and libraries (`.a` or `.so`)
	- if the linker cannot find the definition of a symbol, this step fails with an error
	- `gcc main.c`
	- to view use `objdump -d a.out`

## Static vs Dynamic
#### Static
- If `a.out` *statically* links in library code (from `.a` files), gcc *embeds copies of the library* functions from the `.a` file in the resulting `a.out` file
	- results into a larger executable
	- each proccess gets it's own data copy
	- for any changes the binary should be recompiled
#### Dynamic
- If `a.out` was created by *dynamically linking a library* (from `.so` files) then `a.out` *does not* contain a copy of the library function code. Such executables require an additional step

##### Runtime linking 
- The dynamic library code must be *loaded at runtime* and *linked with the running program*
- This process happens before the execution of the `main` function
- `ldd` lists an executable file's shared object dependencies.
	- `ldd a.out`
- *Procedure Lookup Table* (PLT) - used for runtime linking of calls to dynamically linked library functions. #look_into


## Common Compilation Errors Releated to Compiling and Linking Libraries

"The *extern* prefix to the function prototype means that the function’s
definition comes from another file—it’s not in the examplelib.h file, but in
stead it’s provided by one of the .c files in the library’s implementation."

- forget to include the library header files
- forget to explicitly link in library code
- `gcc` can't find header or library files
- `gcc` can't find the path
	- specify it using `-I` for headers and `-L` for libraries
	- ` gcc -I/home/me/include -o myprog myprog.c -L/home/me/lib -lexamplelib`
	- look into *Makefile*.

## Writing and Using Your Won C LIbraries 

To create a library in C:
1. Define an interface in header (`.h`) files
2. Create an implementation in `.c` files
3. Compile a binary of the library that can be linked into programs (*dynamically* or *statically*)

#### Define the library interface

```c
// mylib.h

#ifndef _MYLIB_H_

#define _MYLIB_H_
#define BEST_NUM 3

struct foo{
	int bar;
};

extern int totalSum;  
extern void sayHi();

#endif
```
- `#ifndef-#endif` block ensures that the contents of `_MYLIB_H_` are included only once


#### Implement the library functionaity

```c
// mylib.c

#include <stdio.h>
#include "mylib.h" // for file that is not in a default library path
  
int totalSum = 100;
void sayHi(){
	printf("Hi\n");
}
```

#### Create a binary form of the library
- `gcc -o mylib.o -c mylib.c` - binary form of the library
- >= 1 `.o` files can build an archive (`.a`) or shared object (`.so`) version of the library.
	- `ar -rcs libmylib.a mylib.o` - to build a static lib (`ar` -> *archiver*)

#### Use the library

```c
// myprog.c

#include <stdio.h>
#include "mylib.h"

int main(){
	printf("Best num is: %d\n", BEST_NUM);
	sayHi();
	totalSum++;
	printf("sum -> %d\n", totalSum);
}

```
- to compile that uses the library (`myli.o`) - `gcc -o myprog myprog.c mylib.o`
- can be also built directly from source - `gcc -o myprog myprog.c mylib.c`
- if the library is an archive or shared object - `gcc -o myprog myproc.c -L. -lmylib`
	- `-L.` -> where to search (in the current directory)
	- dynamically linked version will cause an error because the *linker* can't find `libmylib.so`. 
	- Add it using `export LD_LIBRARY_PATH=/home/me/mylibs:$LD_LIBRARY_PATH`


## Compiling C to Assembly, and Compiling and Linking Assembly and C Code

```c
// main.c
int main() {
	int x, y;
	x = 1;
	x = x + 2;
	x = x - 14;
	y = x*100;
	x = x + y * 6;
	
	return 0;
}
```

- `gcc -m32 -S main.c`
	- `-m32` -> generate *IA32* assembly
	- `-S` -> compile to assembly

```s
--snip--
	movl	$1, -8(%ebp)     # x = 1
	addl	$2, -8(%ebp)     # x += 2
	subl	$14, -8(%ebp)    # x -= 14
	movl	-8(%ebp), %eax   # load x into R[%eax]
	imull	$100, %eax, %eax # into R[%eax] store result of x*100
	movl	%eax, -4(%ebp)   # y = x*100
--snip--
```


#### Write Assembly


```s
	.text             # this file contains instruction code
.globl myfunc         # myfunc is the name of a function
	.type myfunc, @function
myfunc:               # the start of the function
	pushl %ebp        # function preamble:
	movl %esp, %ebp   # the 1st three instrs set up the stack
	subl $16, %esp
	
	# A programmer adds specific IA32 instructions
	# here that allocate stack space for any local variables
	# and then implements code using parameters and locals to
	# perform the functionality of the myfunc function
	#
	# the return value should be stored in %eax before returning
	leave             # function return code
	ret
```
- To use it inside C code
```c
#include <stdio.h>

int myfunc(int param)

int main(){

	int ret;
	ret = myfunc(32);
	printf("myfunc(32) is %d\n", ret);
	return 0;
}

```
- `gcc -m32 -c myfunc.s`
- `gcc -m32 -o myprog myfunc.o main.c`