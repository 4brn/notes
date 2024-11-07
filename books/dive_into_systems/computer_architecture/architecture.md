## 5.2. The von Neumann Architecture

1.  The **processing unit** executes program instructions.
2.  The **control unit** drives program instruction execution on the processing unit. Together, the processing and control units make up the CPU.
3.  The **memory unit** stores program data and instructions.
4.  The **input unit(s)** load program data and instructions on the computer and initiate program execution.
5.  The **output unit(s)** store or receive program results.

- A **bus** is a communication channel that transfers binary values between communication endpoints

## 5.2.1
- CPU -> control + processing units.

## 5.2.2 The Processing Unit
- **arithmetic/logic unit** (ALU) -> performs mathematical & logical operations
- **register** -> small, fast unit of storage used to hold program data and the instructions that are being executed by the ALU


## 5.2.3. The Control Unit
- **control unit** -> loads instructions from memory and feeds them instruction operands and operations
- **program counter** (PC) -> memory address of next instruction
- **instruction register** (IR) -> instruction currently being executed

## 5.2.4. The Memory Unit
- **memory unit** -> stores both program data and program instructions
- 32-bit architectures typically support a maximum address space size of 2^32, which corresponds to 4 gigabytes (GiB) of addressable memory.
- **RAM** -> memory that can be accessed by the CPU
- **word size** -> number of bits a processor handles as a single unit

## 5.2.5. The Input and Output (I/O) Units
- **input unit** -> get data
- **output unit** -> relay results back to the world (monitor, speakers and SSDs!)

## 5.2.6. The von Neumann Machine in Action: Executing a Program

1.  **The control unit _fetches_ the next instruction from memory**.
2.  **The control unit _decodes_ the instruction stored in the IR**. 
3.  **The processing unit _executes_ the instruction**. 
4.  **The control unit _stores_ the result to memory**.

https://academo.org/demos/logic-gate-simulator/