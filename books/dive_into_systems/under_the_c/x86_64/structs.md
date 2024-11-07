- a struct is a collection of data types. Elements are stored contiguously.

```c
typedef struct{
	char name[64];
	int age;
	int grad_yr;
	float gpa;
}Student;
```
![[Pasted image 20221120113723.png]]
- structs in assembly are treated like single-dimensional arrays -> fields are accessed through a base address (the name of the struct) + and offset. 

#### New instructions and registers
```r
movss %xmm0, -0x1(%rbp) 
# movss indicates that the data being moved onto the stack is of type single-precision floating point
# %xmm0 is a register for floating-point values
```

## Data alignment and structs
- if the above code is slightly modified 
```c
typedef struct{
	char name[63];
	int age;
	int grad_yr;
	float gpa;
}Student;
```
- the memory alignment will look like so:
![[Pasted image 20221120115031.png]]
- *x64's alignment policy* requires:
	- 2-byte data types (short) reside at 2-byte-aligned address
	- 4-byte data types (int, float, unsigned) reside at 4-byte-aligned addresses
	- larger data types (long, double, pointers) reside at 8-byte-aligned addresses
	- this can be done by adding **padding** between fields
- values aligned properly in memory can be read or written in a *single operation*