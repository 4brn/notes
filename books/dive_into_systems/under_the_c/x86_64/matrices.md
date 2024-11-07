- matrix -> two-dimensional array
	- can be dynamically allocated with 1 `malloc` call or with multiple (`M[n][m]`).
- memory allocation in assembly using `malloc` 

```r
	.text
	.section	.rodata
.msg:
	.string	"a -> %d\n"
	.text
	.globl	main
	.type	main, @function
main:
.LFB6:
	pushq	%rbp # save %rbp
	movq	%rsp, %rbp # update %rbp
	subq	$16, %rsp # increase the stack by 16 bytes
	movl	$4, %edi # 4 -> %edi (first argument)
	call	malloc@PLT # call malloc(4) -> ask for 4 bytes
	movq	%rax, -8(%rbp) # move the result into -8(%rbp) (it's a pointer)
	movl	$42, (%rax) # dereference %rax and save 42
	movl	(%rax), %eax # %eax = *(%rax)
	movl	%eax, %esi # 2nd arg
	leaq	.msg(%rip), %rdi # 1st arg
	call	printf@PLT # print
	movl	$0, %eax # return = 0
	leave # prepare to leave
	ret # return
```
- a matrix can be *allocated statically* (on the stack). In this case all the elements are stored contiguously. ($x_0,x_4,x_8,x_{12},x_{16},x_{20},\dots$)
```c
int matrix[3][4];
```
- it can also be *allocated dynamically* (on the heap) in a programmer friendly way (doesn't guarantee contiguous ordering)
```c
int** matrix;
matrix = malloc(4 * sizeof(int*));
for(int i = 0; i < 4; i++) matrix[i] = malloc(3 * sizeof(int));
```
- or in memory friendly way (does guarantee contiguous ordering)
```c
int** matrix = malloc(ROWS * COLS * sizeof(int));
```
- follow through the [example](https://diveintosystems.org/book/C7-x86_64/matrices.html#_contiguous_two_dimensional_arrays) given in the book
#### New instructions
```r
movslq %edx,%rdx   # convert %edx to a 64-bit integer and save it into %rdx
shl $0x2, %rdx     # multiply %rdx by 4 using left shift
# 0b11 (3) <left shift 2> -> 0b1100 (8 + 4 = 12)
```