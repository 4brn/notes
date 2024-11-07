> I have read only the x86_64 assembly part

## Common Features
- The *ISA (Instruction set architecture)* defines the assembly language
- Registers hold data:
	- general purpose registers -> hold any kind of data
	- special purpose registers -> specific purpose (base pointer, stack pointer, instruction pointer)
- Instructions specify what the CPU can do:
	- ISA defined *instructions* which specify what can be performed.
		- operation code (*opcode*) -> what the instruction does
		- operands -> the data to be used
- Program stack holds local variables *associated* with a particular function
	- stack pointer & base pointer specify a *stack frame*
	- stack frame removed when function call ends but data is not cleared resulting in *junk values*.
- Security
	- when programming in C use *length specifiers*
	- use Rust
## Further reading 
- Intel systems: [_Computer Systems: A Programmer’s Perspective_](http://csapp.cs.cmu.edu/) (Randal Bryant and David O’Hallaron)
- learn the Intel syntax