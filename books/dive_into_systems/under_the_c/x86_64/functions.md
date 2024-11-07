## 7.5 Functions in Assembly
#### Recall
- `%rsp` -> *stack pointer*, points to the top of the stack
- `%rbp` -> *base pointer/frame pointer*, points to the base of the current *stack frame*.
- **stack frame** (also activation frame or activation record) -> refers to the portion of the stack allocated to a single function call.
	- the currently executing function is on the TOP of the stack
		- it's frame is referred to as the *active frame*
		- bound by (there are stored the local variables of the function)
			- stack pointer `%rsp` at the top
			- frame pointer `%rbp` at the bottom
![[Pasted image 20221118094721.png]]
- first value stored on the stack is a copy of `%rbp`.
- top of activation frame is bounded by the *return address* of the called function.
> the return address points to the code segment memory and not the stack memory

#### Instructions

- `leaveq` - prepares the stack for leaving a function by coping the value of `%rbp` into `%rsp`. Refer to [this](obsidian://open?vault=low-level&file=systems%2Funder_the_c%2Fx86_64%2Fcommon_instructions) for reminder on `push` and `pop`
```r
mov %rbp, %rsp
pop %rbp
```
- `callq addr <fname>` - switches active frame to callee function, saves the `%rip` register and then modifies it. Value of next instruction is pushed onto the stack as a return address.
```r
push %rip
mov addr, %rip
```
- `retq` - restores the active frame to the caller function, any value returned is stored in `%rax`. Usually last instruction.
```r
pop %rip
```

#### Function parameters

|Parameter |Location
--- | --- |
|1|%rdi|
|2|%rsi|
|3|%rdx|
|4|%rcx|
|5|%r8|
|6|%r9|
|7+|on call stack|


### Practical example
- follow through the book [here](https://diveintosystems.org/book/C7-x86_64/functions.html#_tracing_through_an_example)
- `sub $<number>, %rsp` -> subtracts `<number>` from the `%rsp` pointer which makes it bigger (e.g. `sub $0x10, %rsp` subtracts decimal 16 from the stack pointer allowing for two 1-byte variables to be saved).
- values can be pushed onto the stack *without* chainging the value of `%rsp` (adding a local variable)
- *!* old values from the stack are *not* removed when the functions executions ends.


##### Testing

```r
	.file	"nums.c"
	.text
	.section	.rodata
.msg:
	.string	"num -> %d\n"
	.text
	.globl	main
	.type	main, @function
main:
.LFB0:
	pushq	%rbp
	movq	%rsp, %rbp
	subq	$16, %rsp # if this line is commented, prints only once
	movl	$0, -4(%rbp)
	jmp	.L1
.L2:
    movl -4(%rbp), %esi
	leaq .msg(%rip), %rdi
	call	printf@PLT
	addl	$1, -4(%rbp)
.L1:
	cmpl	$10, -4(%rbp)
	jle	.L2
	movl	$0, %eax
	leave
	ret

```
> the above code prints a sequence of numbers
- if the line `subq` is removed



![[Pasted image 20221118125007.png]]

![[Pasted image 20221118125148.png]]