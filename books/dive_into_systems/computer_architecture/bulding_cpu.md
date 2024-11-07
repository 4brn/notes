## 5.5. Building a Processor: Putting It All Together
![[Pasted image 20221109210612.png]]
### 5.5.1 The ALU
- implements all arithmetic and logic operations
- **opcode** - value which specifies the operation to perform
- **condition code** - information about the result 
	- is the result positive, negative or 0
		- each condition is 1 bit
	- is there a carry-out bit
- condition codes are somtimes used by subsecuent instructions to choose what action to do
- in case of an if statement a conditional jump may be done if the condition is false
	- CPU writes the memory address of the first instruction *after the if body* into the *program counter (PC)*
- A fully operational example of an ALU
![[Pasted image 20221109211628.png]]
- the binary encoding for and ADD instruction might consist of 4 parts:
	- opcode bits
	- operand A source
	- operand B source
	- result destination
- there can be more depending on the CPU architecture
- ALU that performs N operations needs log2(N) opcode bits to choose (like a MUX)

### 5.5.2 The Register File
- at the top of the *memory hierarchy* are the CPU general-purpose registers
- instructions get their values from or store the result to registers
	- `add the value from register1 to the value of register2 and store the result at register3`
- general-purpose registers are organized into a **register file** circuit which consists of
	- *register circuits* for storing data
	- *control circuits* for controlling reads and writes
- special-purpose registers
	- **program counter (PC)** - memory address of the next instruction
	-  **instruction register (IR)** - bits of the current instruction

### 5.5.3 The CPU
- The ALU and the Register File circuits are the main parts of the CPU. Data stored in the general-purpose registers goes to the ALU and then the output gets stored back in the general-purpose registers (or main memory). These two parts make the **data path** (plus the buses).
- There is also a **control path** drives the execution of program instructions.