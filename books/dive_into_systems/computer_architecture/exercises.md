### Exercises for 5.4 Circuits


1. Create a 1-bit XOR circuit using only AND, OR, and NOT gates. Explicitly show all steps starting from the truth table for XOR, then listing the logical expressions for when XOR is 1, and then translating the expressions into a circuit.
	- truth table
	
	|A |B  | OUTPUT |
	--- | --- | --- |
	|0|0|0|
	|0|1|1|
	|1|0|1|
	|1|1|0|	

		```
		A OR B # for rows 2 and 3
		NOT(A AND B) # so 1 1 is 0
		
		A OR B AND NOT(A AND B)
		A OR B AND NOT(A) OR NOT(B) # De Morgans theorem
		
		```
	![[Pasted image 20221110022815.png]]

2. List the truth table for the full 1-bit adder circuit with 3 input values (A, B, and CARRY IN), and two output values (SUM and CARRY OUT).

	|A |B | IN | SUM| OUT |
	--- | --- | --- | ---| ---|
	|0|0|0|0|0|
	|1|0|0|1|0
	|0|1|0|1|0
	|0|0|1|1|0
	|1|1|0|0|1	
	|1|0|1|0|1	
	|0|1|1|0|1	
	|1|1|1|1|1		

3. Create a 4-bit negation circuit using only basic logic gates (AND, OR, NOT), and a 1-bit adder circuit. Assume that the high-order bit (bit 3) is the sign bit of the two’s complement 4-bit values. Refer to [Chapter 4](https://diveintosystems.org/book/C4-Binary/signed.html#_signed_binary_integers) for details on negation of two’s complement numbers.
	- create a 4-bit adder 	
	![[Pasted image 20221110031232.png]]
	- 4-bit negation circuit
![[Pasted image 20221110031543.png]]
![[Pasted image 20221110031935.png]]
- version with only adders

1. For the [4-way multiplexer circuit shown in the Control Circuits section](https://diveintosystems.org/book/C5-Arch/controlcircs.html#Fig4waymux), explain why an S input value of 1 results in the multiplexer outputting B’s value.
	- A 4 way multiplexer needs log2(4) = 2 bits for Select(S) inputs to represent all variations. By making the S input 1 (S0 = 1, S1 = 0) the 3AND that is connected to the B input is the only one powered twice for sure which leaves `B AND 1 AND 1` which is `B`.
2. How many selection bits are needed for a 16-way multiplexer? Explain your answer.
	- An N-way multiplexer needs log2(N) selection bits to represent all possible variants this a 16-bit MUX needs log2(16) = 4 (S)election bits.
3. Draw an RS latch circuit that stores 0. Then, trace through the updates to the circuit to write 1 into it. Use the [RS latch figure in the Storage Circuits section](https://diveintosystems.org/book/C5-Arch/storagecircs.html#Figwrite0), as an example.
	![[Pasted image 20221110025107.png]]
	- turn off (0) `R` and then turn it on (1). This will result in `Q` being on(1)
	- Both `R` and `S` should never be off at the same time
	![[Pasted image 20221110025211.png]]
7. For the [figure of the gated D latch shown in the Storage Circuits section](https://diveintosystems.org/book/C5-Arch/storagecircs.html#FiggatedD), what input values result in writing 1 into the latch? What inputs result in writing 0 into the latch?
	- the Data D input should be 1 and the WE WriteEnable should be 1 as well, this will write 1 into the latch. The Data D input should be 0 and WE 1 to write 0 into the latch.
8. Explain why the D input to the gated D latch has no affect on the value stored in the latch when the WE input is 0.
	- the WE WriteEnabled input enables or disables write acces to the latch by blocking two NAND gates.