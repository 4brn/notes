
### Most common
- `mov S, D`: S -> D
- `add S, D`: S + D -> D
- `sub S, D`: D - S -> D

#### Example
```r
mov -0x4(%rbp), %eax
add $0x2, %eax
```
- dereference `-4 + %rbp` and copy the value at the address into `%eax`
- add `2` to `%eax`
> the above 3 instructions are the building blocks for *call stack* management


#### Stack management
- `%rsp` points to the top of the stack
- the stack grows towards *lower* addresses
![[Pasted image 20221110130924.png]]
- by knowing this we can `sub` a value from the stack pointer `%rsp` and enlarge it and then `mov` a value on the top of the stack
```r
sub %0x8, %rsp
mov S, (%rsp)
```
- this can be simplified with
```r
push S
```
- which pushes a copy of S onto the TOP of the stack
- similar idea is with popping things from the stack
```r
mov (%rsp), D
add $0x8, %rsp
```
- pops the top and moves the element to location `D`
- adds `$0x8` to the stack thus making it smaller
- equivalent to
```r
pop D
```

#### Common
- the final values in registers `%rsp` and `%rbp` are the same as at the beginning of a function execution. Because of that it's common to see 
```r
push %rbp
mov %rsp, %rbp
```
- as common first instructions and 
```r
pop %rbp
retq
```
- as last ones

### Misc
> useful commands when using gdb for assembly learning
```
disassemble main
b main
info registers
set %eax=0
```