## 7.4 Conditional Control and Loops
- compiler translates conditionals into assembly that modify the `%rip` register

### 7.4.1 Preliminaries
- `cmp R1, R2` - compare -> eval `R1 - R2`
- `test R1, R2` - performs bitwise AND
	- `cmp $0, %rax`  == `test %rax, %rax`
> don't change the destination register but modify the condition code flags
-  **condition code flags** - series of single-bit values
	- example flags
		- `ZF` - is equal to
		- `SF` - is negative
		- `OF` - overflow
		- `CF` - arithmetic carry

#### Jump instructions
- allow to "jump" to a new position by changing the value of the `%rip` register.
- `jmp L` - jump to location `L`
	- `L` - symbolic label, an identifier in the program's object file
		- `main:` - *global label*, used for functions
		- `.L1:` - *local label*, used for `if` statements or loops
			- can be represented as an offset from the start of the function - `<main+28>` 
				- `jmp 0x8048427 <main+28>` -> jumps to `0x8048427` which is 28 bytes from the start of main
- `jmp *addr` - jump to address

#### Conditional jump instructions
- depends on the *condition code registers* set by `cmp`.
- `je (jz)` -> == or == 0
- `jne (jnz)` -> != 
- `js` -> negative
- `jns` -> non-negative
- `jg (jnle)` -> >
- `jge (jnl)` -> >=
- `jl (jnge)` -> <
- `jle (jng)` -> <=
> greater and less use signed value, above and below use unsigned


### 7.4.2 if Statement in Assembly
- practical exercise, follow the book.
> gcc places first and second parameters in `%rdi` and `%rsi`
- #look_into `__attribute__((naked))`
- a function written in different ways in C can result in the same assembly code

#### The cmov instruction
- `cmp`, `test` and `jmp` implement *conditional transfer of control* while `cmov` implements *conditional trnasfer of data*.
- C's **ternary expressions** often result in `cmov`
	- `res = (condition) ? then_statement : else_statement;` 
- the `cmov` instruction copies destination to source depending on the *condition code flags*.
```r
0x4005d7 <+0>:   push   %rbp             #save %rbp
0x4005d8 <+1>:   mov    %rsp,%rbp        #update %rbp
0x4005db <+4>:   mov    %edi,-0x4(%rbp)  #copy x to %rbp-0x4
0x4005de <+7>:   mov    %esi,-0x8(%rbp)  #copy y to %rbp-0x8
0x4005e1 <+10>:  mov    -0x8(%rbp),%eax  #copy y to %eax
0x4005e4 <+13>:  cmp    %eax,-0x4(%rbp)  #compare x and y
0x4005e7 <+16>:  cmovle -0x4(%rbp),%eax  #if (x <=y) copy x to %eax
0x4005eb <+20>:  pop    %rbp             #restore %rbp
0x4005ec <+21>:  retq                    #return %eax
```
- refer to the lesson for a table of all instructions
> compiler's internal optimizer will replace `jmp` instructions with `cmov` instruction if level 1 optimization (`-01`) is turned on
- `gcc -O1 -o getSmallest getSmallest.c` 
-  compiler is very cautious when replacing `jmp` instructions with `cmov` ones as it can lead to errors:
	- e.g. -> if there is a pointer which might be `NULL` if `cmov` is used it will execute both instructions which can lead to dereferencing a null pointer.


#### Additional
- experiments from me

```c
int inc(int* x){
    return x ? (*x)++ : 1;
}

int main(){
    int a = 1;
    inc(&a);

    return 0;
}
```

```r
# the inc function from above

0x0000555555555139 <+0>:	push   %rbp 
0x000055555555513a <+1>:	mov    %rsp,%rbp 
# int*x -> -0x8(%rbp)
0x000055555555513d <+4>:	mov    %rdi,-0x8(%rbp) 
# check for null pointer
0x0000555555555141 <+8>:	cmpq   $0x0,-0x8(%rbp) 
# if -0x8(%rbp) == 0(NULL) go to inc+32
0x0000555555555146 <+13>:	je     0x555555555159 <inc+32> 
# move the *x pointer to %rax 
0x0000555555555148 <+15>:	mov    -0x8(%rbp),%rax
# dereference the address stored at %rax (*x) and move it to %eax
0x000055555555514c <+19>:	mov    (%rax),%eax
# %eax = *x + 1
0x000055555555514e <+21>:	lea    0x1(%rax),%ecx
# move the address of x to %rdx
0x0000555555555151 <+24>:	mov    -0x8(%rbp),%rdx
# *x = %eax
0x0000555555555155 <+28>:	mov    %ecx,(%rdx)
# jump to inc+37
0x0000555555555157 <+30>:	jmp    0x55555555515e <inc+37>
# put 1 into %eax
0x0000555555555159 <+32>:	mov    $0x1,%eax
0x000055555555515e <+37>:	pop    %rbp
0x000055555555515f <+38>:	ret
```


### 7.4.3 Loops in Assembly

```r
0x400554 <+0>:   push   %rbp                   #save %rbp
0x400555 <+1>:   mov    %rsp,%rbp              #update %rpb (new stack frame)
0x400558 <+4>:   mov    %edi,-0x14(%rbp)       #copy %edi to %rbp-0x14 (n)
0x40055b <+7>:   movl   $0x0,-0x8(%rbp)        #copy 0 to %rbp-0x8 (total)
0x400562 <+14>:  movl   $0x1,-0x4(%rbp)        #copy 1 to %rbp-0x4 (i)
0x400569 <+21>:  jmp    0x400575 <sumUp2+33>   #goto <sumUp2+33>
0x40056b <+23>:  mov    -0x4(%rbp),%eax        #copy i to %eax [loop]
0x40056e <+26>:  add    %eax,-0x8(%rbp)        #add i to total (total+=i)
0x400571 <+29>:  addl   $0x1,-0x4(%rbp)        #add 1 to i (i++)
0x400575 <+33>:  mov    -0x4(%rbp),%eax        #copy i to %eax [start]
0x400578 <+36>:  cmp    -0x14(%rbp),%eax       #compare i with n
0x40057b <+39>:  jle    0x40056b <sumUp2+23>   #if (i <= n) goto loop
0x40057d <+41>:  mov    -0x8(%rbp),%eax        #copy total to %eax
0x400580 <+44>:  pop    %rbp                   #prepare to leave the function
0x400581 <+45>:  retq                          #return total
```
- uses `cmp` and `jmp` instructions to jump to an address while a variable is being incremented. `while` and `for` loops can yield the same result in assembly