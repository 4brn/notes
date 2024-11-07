## 5.7. Pipelining: Making the CPU Faster
- four-stage (fetch, decode, execute, safe) CPU takes four cycles to execute one instruction
- to execute N instructions 4N clock cycles are needed.
- this can be improved as some parts do not do anything (e.g. after the fetch stage, the fetch circuitry does nothing)
- CPU **pipelining** - starting the execution of the next instruction before the current instruction is fully done.
![[Pasted image 20221109233633.png]]
- this leads to *CPI* of 1!
- total number of cycles required to execute a single instruction - instruction **latency**
- number of instructions a CPU can execute in a given period of time by *overlapping* the execution of sequential instructions in a staggered manner, through the different stages of the pipeline - **throughput**