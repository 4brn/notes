- Notes for [this](https://www.cs.swarthmore.edu/~newhall/unixhelp/howto_makefiles.html) resource.
- simplify the development process, do not recompile if there are no changes.
## Using make
- create a file named `Makefile` or `makefile`
- type `make` to rebuild
## Creating a Makefile
- makefiles generally follow this structure

```makefile
# comment
# (note: the <tab> in the command line is necessary for make to work) 
target:  dependency1 dependency2 ...
      <tab> command

for example:
#
# target entry to build program executable from program and mylib 
# object files 
#
program: program.o mylib.o
	gcc -o program program.o mylib.o
```
- an example for a simple `C` program
```makefile
  # the compiler: gcc for C program, define as g++ for C++
  CC = gcc

  # compiler flags:
  #  -g    adds debugging information to the executable file
  #  -Wall turns on most, but not all, compiler warnings
  CFLAGS  = -g -Wall

  # the build target executable:
  TARGET = myprog

  all: $(TARGET)

  $(TARGET): $(TARGET).c
  	$(CC) $(CFLAGS) -o $(TARGET) $(TARGET).c

  clean:
  	$(RM) $(TARGET)
```
- using makefiles works great with VScode.
- run `make clean` to invoke the clean part and remove the *ELF*.
- here is a more complex example for multiple files

```makefile
#
# This is an example Makefile for a countwords program.  This
# program uses both the scanner module and a counter module.
# Typing 'make' or 'make count' will create the executable file.
#

# define some Makefile variables for the compiler and compiler flags
# to use Makefile variables later in the Makefile: $()
#
#  -g    adds debugging information to the executable file
#  -Wall turns on most, but not all, compiler warnings
#
# for C++ define  CC = g++
CC = gcc
CFLAGS  = -g -Wall

# typing 'make' will invoke the first target entry in the file 
# (in this case the default target entry)
# you can name this target entry anything, but "default" or "all"
# are the most commonly used names by convention
#
default: count

# To create the executable file count we need the object files
# countwords.o, counter.o, and scanner.o:
#
count:  countwords.o counter.o scanner.o 
	$(CC) $(CFLAGS) -o count countwords.o counter.o scanner.o

# To create the object file countwords.o, we need the source
# files countwords.c, scanner.h, and counter.h:
#
countwords.o:  countwords.c scanner.h counter.h 
	$(CC) $(CFLAGS) -c countwords.c

# To create the object file counter.o, we need the source files
# counter.c and counter.h:
#
counter.o:  counter.c counter.h 
	$(CC) $(CFLAGS) -c counter.c

# To create the object file scanner.o, we need the source files
# scanner.c and scanner.h:
#
scanner.o:  scanner.c scanner.h 
	$(CC) $(CFLAGS) -c scanner.c

# To start over from scratch, type 'make clean'.  This
# removes the executable file, as well as old .o object
# files and *~ backup files:
#
clean: 
	$(RM) count *.o *~
```
> these are just the basics of Makefiles

