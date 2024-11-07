
## 5.4.1 Arithmetic and Logic Cicruts
- make the *ALU (Arithemtic/Logic Unit)* of the processor as well as other parts such as the *PC (Programs Counter)*.

### Designing a circut
> start small by making a 1-bit version which is then used as the building block for M-bit version.

1. Design the truth table
2. Using the truth table, write an expression for when each circuit output is 1 in terms of its input values combined with AND, OR, NOT.
3. Chain the logic gates

#### Example -> 1-bit equals circut
1. Truth table

	|A |B  | OUTPUT |
	--- | --- | --- |
	|0|0|1|
	|0|1|0|
	|1|0|0|
	|1|1|1|	
2. Write an expressions 
	- construct a **conjunction** (subexpressions that evaluate to 0 || 1 with AND and is itself 1 only when both subexpressions are 1) 
		- 1st row
			```
			NOT(A) # is 1 when A is 0
			NOT(B) # is 1 when B is 0
			NOT(A) AND NOT(B) # is 1 when A and B are both 0	
			```
		- 4th row
			```
			A # is 1 when A is 1
			B # is 1 when A is 1
			A AND B # is 1 when both A and B are 1
			```
	- Create a **disjunction** (OR) of each conjunction that evaluates to 1.
		- `(NOT(A) AND NOT(B)) OR (A AND B) # combines both`
	- That's the final expression which now should be simplified if possible and then the circut should be constructed.
	- Be careful when simplifying the expression (`NOT(A) AND NOT(B)` != `A NAND B` )
3. Create the circuit
	- start from the innermost gates (the ones closest to the input)
	- test the correctness of the circuit by running every permutation
4. The circuit can then be used as an abstraction (like a function).

#### Exercise -> 1-bit adder
> input -> A and B
> output -> SUM and CARRY OUT

1. Table

	| A | B | SUM | CARRY OUT |
	---| ---| ---| ---|
	|0|0|0|0|
	|1|0|1|0|
	|0|1|1|0|
	|1|1|0|1|
2. Expressions
```
A XOR B # for SUM to be 1
A AND B # for CARRY OUT to be 1
```

#### Exercise -> 1-bit adder with CARRY IN
> this can be later used for N-bit adder

1. Table

| A | B | CARRY IN |SUM | CARRY OUT |
---| ---| ---| ---|---|
|0|0|0|0|0
|1|0|0|1|0
|0|1|0|1|0
|0|0|1|1|0
|1|1|0|0|1
|0|1|1|0|1
|1|0|1|0|1
|1|1|1|1|1

2. Expression
```
# CARRY IN => IN

# FOR SUM
((A AND B) AND IN) # ALL are in
A XOR IN AND NOT(B)
B XOR IN AND NOT(A)
A XOR B AND NOT(IN)

((A AND B) AND IN) OR (A XOR IN AND NOT(B)) OR (B XOR IN AND NOT(A)) OR (A XOR B AND NOT(INT)) # FOR SUM

# FOR CARRY OUT

(A AND B)
(A AND IN)
(B AND IN)
((A AND B) AND IN)

(A AND B) OR (A AND IN) OR (B AND IN) OR ((A AND B) AND IN) # FOR CARRY OUT

```
![[Pasted image 20221109140448.png]]
- try simplifying it using the normal 1 bit adder
##### BETTER SOLUTION

![[Pasted image 20221109142826.png]]
- this solution is from Sebastian's video.
```
# Expression (from me)
(A XOR B) XOR IN -> SUM
((A XOR B) AND IN) OR (A AND B) -> CARRY OUT
```
- to simplify such expressions **boolean algebra** is needed.
- by combining the 1-bit adders a N-bit adder can be made - a *ripple carry adder* (the sum ripples or propagates through the circuit)