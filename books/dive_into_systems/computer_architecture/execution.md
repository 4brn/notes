## 5.6. The Processor’s Execution of Program Instructions

- depending on the architecture there can be different number of stages but the most common are **Fetch, Decode, Execute and WriteBack**.
![[Pasted image 20221109225813.png]]

- fetch - instruction at memory address is read and stored into the *IR (instruction pointer)*, *PC (program counter)* is incremented.
- decode - separate the instruction bits in the *IR (instruction pointer)* into components and send them to the ALU (Arithmetical/Logical unit).
	- opcode bits
	- two sets of operand bits
	- destination bits
- execute - the ALU performs the specified operation
- write back  - the result (output from ALU) is written to the destination register


## 5.6.1 Clock-Driven Execution
- a clock drives the CPU's execution of instructions
- **clock cycle time** - measures the time between each *clock tick*.
- A processor's **clock speed (clock rate)** is 1/(*clock cycle time*)(GHz) -> 1 billion ticks per second.
- When increasing the clock rate problems associated with heat start to araise. This limit is know as **power wall** . A workaround is to make *multicore* processors that have multiple "simple" CPU cores per chip, each with a clock.
#### The Clock Circuit
- oscillator circuit generates a very precise and regular *pulse pattern*.
- **clock cycle** or **tick** - 1 and 0 subsequence
	- the transition from 1 to 0 or from 0 to 1 is **clock edge**
	- *clock edges* trigger execution of instructions
		- *falling edge* - 1 -> 0
		- *rising edge* - 0 -> 1
- **propagation delay** - time between the change of the clock (1 & 0).
- **cycles per instruction** (CPI) - average number of cycles to execute an instruction
