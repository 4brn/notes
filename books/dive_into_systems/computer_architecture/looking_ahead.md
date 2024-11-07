
## 5.9. Looking Ahead: CPUs Today
- **instruction-level parallelism (ILP)** - CPU simultaneously executes multiple instructions in parallel.
- **Instructions per cycle (IPC)** - performance metric
- **Cycles per instruction (CPI)** - performance metric
- **Moore's Law** - transistors per integrated circuit double every 1 or 2 years
	- number of transistors that can fit on a chip is a rought measure of performance
### 5.9.1. Instruction-Level Parallelism
- *Instruction-Level Parallelism (ILP)* is transparent to the programmer as the programmer writes sequential C but the processor executes several instructions in parallel.
- **vector processor** - implements ILP through special vector instructions that take one-dimensional arrays (vectors) of data as their operands. Today this architecture is mainlt used in accelerator devices (*GPUs*) that are optimized for performing computation on image data stored in 1D arrays.
- **superscalar** - fetches a set of instructions, breaks them into multiple independennt streams which are executed in parallel. This is an **out-of-order processor** as the instructions are executed out of order. Needs to perform *dependency analysis* to see if there can be any problem with out of order execution. Fast but not always.
- **Very long instruction word (VLIW)** - similar to *superscalar* however the compiler is responsible for constructing the multiple independent instruction streams. Eliminates the need of *dependenciy analysis* later on. Requires special compiler
	- both *superscalar* and *very long instruction word* are limited because of the sequencial nature of the programs and the dependencies between instructions.
### 5.9.2. Multicore and Hardware Multithreading
- require _explicit parallel programming_ by a programmer
- **Hardware multithreading** - single-processor design, multiple hardware threads.
	- **thread** - independent stream of execution 
	- **explicitly multithreaded** - support fetching instructions from multiple separate instruction streams
	- *IPC (Instructions per Cycle)* > 1
	- Multithreaded architectures based on simple scalar processors implement **interleaved multithreading** - (cannot into IPC > 1), single ALU
	- Hardware threading supported by superscalar-based microarchitectures is often called **simultaneous multithreading** (SMT)
- **Multicore processors** contain multiple *complete CPU cores*
	- like multithreaded processors, each core is independently scheduled by the OS
	- each core of a multicore processor could be scalar, superscalar, or hardware multithreaded
![[Pasted image 20221110015310.png]]

- check out the additional resources at the end of the chapter