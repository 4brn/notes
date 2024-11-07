## 5.8. Advanced Pipelined Instruction Considerations
> recall -> pipelining improves the performance of a processor by overlapping the execution of multiple instructions

#### Five-stage pipeline
-   **Fetch (F):** reads an instruction from memory (pointed to by the program counter).
-   **Decode (D):** reads source registers and sets control logic.
-   **Execute (E):** executes the instruction.
-   **Memory (M):** reads from or writes to data memory.
-   **WriteBack (W):** stores a result in a destination register.

> recall -> compiler transforms code to series of machine code instructions

```r
MOV M[0x84], Reg1     # move value at memory address 0x84 to register Reg1
ADD 2, Reg1, Reg1     # add 2 to value in Reg1 and store result in Reg1
MOV 4, Reg2           # copy the value 4 to register Reg2
ADD Reg2, Reg2, Reg2  # compute Reg2 + Reg2, store result in Reg2
JMP L1<0x14>          # jump to executing code at L1 (code address 0x14)
```
- every *ISA (Instruction Set Architecture)*
- each instruction *operates* on >= 1 *operands
- not all instructions require the same number of pipeline stages to execute
	- `MOV` requires all 5 (moves data from memory to register)
	- `JMP` requires only 3 (F, D, E) as it doesn't update a general-purpose register
- A **pipeline stall** results when any instruction is forced to wait for another to finish executing before it can continue.
### 5.8.1. Pipelining Consideration: Data Hazards
- **data hazard** occures when two instructions attempt to access common data
```r
MOV M[0x84], Reg1     # move value at memory address 0x84 to register Reg1
ADD 2, Reg1, Reg1     # add 2 to value in Reg1 and store result in Reg1
```
![[Pasted image 20221109235358.png]]
- both instructions will attempt to write at the same time
- to prevent this the processpr forces every instruction to take 5 pipeline stages by adding a **no-operation (NOP)** instruction (also called "bubble").
- a problem can still occure if an instruction depends on the previous one (needs to read data which hasn't been writtem)
```r
MOV 4, Reg2           # copy the value 4 to register Reg2
ADD Reg2, Reg2, Reg2  # compute Reg2 + Reg2, store result in Reg2
```
![[Pasted image 20221109235810.png]]
- instead of adding more bubbles processors use **operand forwarding** which allows and inctruction to read the result of a previous operation.
### 5.8.2. Pipelining Hazards: Control Hazards
- the pipline is optimized for sequencial instructions but problems arise when there are loops or conditional logic

```c
int result = *x; // x holds an int
int temp = *y;   // y holds another int

if (result <= temp) {
	result = result - temp;
}
else {
	result = result + temp;
}
return result;
```

```r
  MOV M[0x84], Reg1     # move value at memory address 0x84 to register Reg1
  MOV M[0x88], Reg2     # move value at memory address 0x88 to register Reg2
  CMP Reg1, Reg2        # compare value in Reg1 to value in Reg2
  JLE L1<0x14>          # (Jump less than) if Reg1 < Reg2 JMP to L1
  ADD Reg1, Reg2, Reg1  # compute Reg1 + Reg2, store result in Reg1
  JMP L2<0x20>          # switch code execution to L2 (code address 0x20)
L1:
  SUB Reg1, Reg2, Reg1  # compute Reg1 - Reg2, store in Reg1
L2:
  RET                   # return from function
```
- A **control hazard** occurs when the pipeline encounters a branch (or conditional) instruction. When reaching the branch, inctructions have already been added to the *pipeline*. If the branch is taken, the *junk* instructions need to be removed or *flushed* but flushing ain't cheap.
- Possilbe solutions
	- **Stall the pipeline** - add lots of NOP (no operation) bubbles and stall the pipeline until the processsor is sure that the branch is take, leads to performance hits
	- **Branch prediction** - add a **branch predictor** which will predict which way the branch will go, has lead to security vulnarabilities ([Spectre](https://arstechnica.com/gadgets/2019/02/google-software-is-never-going-to-be-able-to-fix-spectre-type-bugs/)).
	- **Eager execution** -execute both sides of the branch and perform conditional data transfer, not all code is capable of taking the advantage of eager execution which can be dangerous in case of pointer derederences and side effects.