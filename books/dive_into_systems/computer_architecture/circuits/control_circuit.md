
## 5.4.2 Control Circuits
- Control circuits are used throughput the system, they:
	- drive the execution of program instructions
	- control loading and storing values
### Multiplexer (MUX)
**nultiplexer (MUX)** - chooses from serveral values 
	- N input values
	- 1 output value
	- *Select (S)* value which decides which input to choose.
- Truth table

|A |B |S | OUTPUT |
---|---|---|--- |
|0|0|0|0 (B's value)
|0|1|0|1 (B's value)
|1|0|0|0 (B's value)
|1|1|0|1 (B's value)	
|0|0|1|0 (A's value)
|0|1|1|0 (A's value)
|1|0|1|1 (A's value)
|1|1|1|1 (A's value)	
- expression - `OUT = (S AND A) OR (NOT(S) AND B)`

![[Pasted image 20221109182223.png]]
- The *two-way 1-bit multiplexer (MUX)* can be then used to build *N-bit MUX* with N inputs and one S to choose which of the two to use.
![[Pasted image 20221109183327.png]]
- here the `S` switch controlls wether the output of the As should be used or the one of the Bs.
- A *N-way multiplexer* chooses one of N inputs as outputs and requires *log2(N) bits* for Select(S) input.
- An example of a *four-way 1-bit MUX* (uses logs(4) = 2 bits for the S input)
![[Pasted image 20221109192017.png]]

#### Demultiplexer
- **demultiplexer (DMUX)** - inverse of a multiplexe -> chooses one of N outputs. IT has 1 input, 1 seclection input and N outputs. Based on S it sends the input to one of the outputs.
- Truth table

|A |S |Out_0 | Out_1 |
---|---|---|--- |
|0|0|0 (A)|0 
|1|0|1 (A)|0
|0|1|0|0 (A)
|1|1|0|1 (A)	

#### Decoder
- **decoder** - takes an encoded input and enables one of several outputs.
	- e.g. - has N-bit input, enables 1 of it's 2^N outputs
- truth table

|In |Out_0 |Out_1 | Out_2 | Out_3|
---|---|---|--- |---|
|0 0|1|0|0|0
|0  1|0|1|0|0
|1 0|0|0|1|0
|1 1|0|0|0|1	