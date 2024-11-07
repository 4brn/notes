```c
#include <stdio.h>

//adds two to an integer and returns the result
int adder2(int a) {
    return a + 2;
}

int main(){
    int x = 40;
    x = adder2(x);
    printf("x is: %d\n", x);
    return 0;
}
```

```r
  0000000000400526 <adder2>:
  400526:       55                      push   %rbp
  400527:       48 89 e5                mov    %rsp,%rbp
  40052a:       89 7d fc                mov    %edi,-0x4(%rbp)
  40052d:       8b 45 fc                mov    -0x4(%rbp),%eax
  400530:       83 c0 02                add    $0x2,%eax
  400533:       5d                      pop    %rbp
  400534:       c3                      retq
	/\          /\                          /\
	||          ||                          ||
address of     instruction               instruction
instruction     in hex
```
- 1 line of C code often translates to >= 1 assembly instructions.

## 7.1.1 Registers
- Intel CPU has 16 registers
- `%rsp` - **stack pointer** - points to the top of the stack
- `%rbp` - **frame/base pointer** - base of the active stack frame, helps reference parameters (locations on the stack)
- `%rip` - **instruction pointer** or **program counter (PC)** - points to the next instruction
- `%rax` - used for **return** value of functions
- `%rdi` - first function **parameter**
- all other registers hold general-purpose data

- x86-64 -> extension of 32-bit x86 architecture -> extension of 16-bit x86
	- ISA provides a mechanism to access the lower bytes
- to access the 32 bits of the first 8 registers change the `r` to `e` (`%rax` -> `eax`)
- to access the lower 16 bits reference the last 2 letters (`%rax` -> `%ax`)
- to access the 8-bit components (*higher* or *lower* bytes), take last 2 letters  and replace last letter with `h` for *higher* and `l` for *lower* (`%ax` -> `%al` for lower and `%ah` for higher)
![[Pasted image 20221110120733.png]]
> compiler may use 32-bit component registers mixed with 64-bit ones (int is stored in `%eax` as it needs 4 bytes)
- last eight bytes (`%r8 - %r15`) were not part of IA32 ISA.
	- `+d` -> lower 32 bits (`%r9 -> %r9d`)
	- `+w` -> lower 16 bits (`%r9 -> %r9w`)
	- `+b` -> lowest byte (`%r9 -> %r9b`)

### 7.1.3. Instruction Structure
- **opcode** - the action
- **operands** - the ones whom the action is done upon
	- `add $0x2, %eax` -> `add` (opcode) `$0x2` (operand, source) to `%eax` (operand, destination)
	- types of operands:
		- **constant (literal)** - ones with a `$`
		- **register** - individual registers
		- **memory** - value inside RAM -> `mov -0x4(%rbp),%eax` -> subtract 4 from `%rbp` and perform a memory lookup (dereference)
- examples
	- `%rcx` -> value of register (register)
	- `(%rcx)` -> value at the memory address of the register (dereference)
### Instruction suffix
- there is a suffix which indicates the size of the data
![[Pasted image 20221110164539.png]]