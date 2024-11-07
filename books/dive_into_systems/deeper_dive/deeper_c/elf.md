# [Executable and Linkable Format](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)

- *Executable and Linkable Format* (*ELF*) -> standart file format for executables, object code, shared libraries and core dumps.
- Standart binary file format for *Unix* and *Unix-like* systems.
	- supports different *endiannesses* and address sizes

## File layout
- ELF file -> ELF *header* followed by file data

### The Data
-   Program header table, describing zero or more [memory segments](https://en.wikipedia.org/wiki/Memory_segmentation "Memory segmentation")
-   Section header table, describing zero or more sections
-   Data referred to by entries in the program header table or section header table
![[Pasted image 20221023115340.png]]


### The Header
- defines whether to use *32-bit* or *64-bit* addresses.
	- ELF header is 52 or 64 bytes long for 32-bit and 64-bit binaries respectively