- recursive functions call themselves (*self-referential*)
- finds the sum of 1...n using recursion
- use [this](https://diveintosystems.org/book/C7-x86_64/recursion.html#_animation_observing_how_the_call_stack_changes) animation to see how the stack changes

```r

	.file	"main.c"
	.text
	.globl	sumr
	.type	sumr, @function
sumr:
.LFB0:
	pushq	%rbp # save %rbp
	movq	%rsp, %rbp # update %rbp
	subq	$16, %rsp # expand the stack by 16 bytes
	movl	%edi, -4(%rbp) # n -> -4(%rbp)
	cmpl	$0, -4(%rbp) # n == 0
	jg	.L2 # if greater jump
	movl	$0, %eax # if n == 0 return 0
	jmp	.L3
.L2:
	movl	-4(%rbp), %eax # n -> %eax
	subl	$1, %eax # %eax--
	movl	%eax, %edi # %eax -> %edi (prepare to call the function again)
	call	sumr # recursive call!
	movl	-4(%rbp), %edx # n -> %edx
	addl	%edx, %eax # %eax += %edx (n += sumr(result))
.L3:
	leave # prepare to leave
	ret # return result
.LFE0:
	.size	sumr, .-sumr
	.section	.rodata
.LC0:
	.string	"a -> %d\n"
	.text
	.globl	main
	.type	main, @function
main:
.LFB1:
	pushq	%rbp # save %rbp
	movq	%rsp, %rbp # update %rbp
	subq	$16, %rsp # expand stack
	movl	$5, %edi # 5 -> %edi
	call	sumr # call function
	movl	%eax, -4(%rbp) # result from function (%eax) -> -4(%rbp)
	movl	-4(%rbp), %eax # -4(%rbp) -> %eax
	movl	%eax, %esi # load result from function into 2nd arg
	leaq	.LC0(%rip), %rax # load the strign address
	movq	%rax, %rdi # move string to %rdi
	movl	$0, %eax # 0 -> %eax
	call	printf@PLT # print result
	movl	$0, %eax # return 0;
	leave # prepare to leave
	ret # done

```

- fibonachi in assembly
```r
	.globl	fib
	.type	fib, @function
fib:
.LFB0:
	pushq	%rbp
	movq	%rsp, %rbp
	subq	$32, %rsp
	movl	%edi, -20(%rbp) # save arg n
	cmpl	$1, -20(%rbp) # n == 1
	jg	.L2 # > jump
	movl	-20(%rbp), %eax
	jmp	.L3
.L2:
	movl	-20(%rbp), %eax # n -> %eax
	subl	$1, %eax # %eax--
	movl	%eax, %edi # pass %eax as arg
	call	fib # call
	movl	%eax, -8(%rbp) # func res a -> -8(%rbp)
	movl	-20(%rbp), %eax # n -> %eax
	subl	$2, %eax # %eax -= 2
	movl	%eax, %edi # load n again
	call	fib # call
	movl	%eax, -4(%rbp) # func res b -> -4(%rbp)
	movl	-8(%rbp), %edx # b -> %edx
	movl	-4(%rbp), %eax # a -> %eax
	addl	%edx, %eax # %eax + %edx


```