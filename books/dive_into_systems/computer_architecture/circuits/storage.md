## 5.4.3 Storage Circuits

- **Storage circuits** are used to construct computer memory such as:
	- **static RAM (SRAM)** 
		- go brrrrrrr
	- CPU register storage and on-chip memory
	- has an input and stored value
- **dynamic memory (DRAM)** is used for main memory (RAM) storage.
	- built using capacitors
	- requires to be peridodically refreshed (thus dynamic)
	- slower but cheaper


#### RS Latch
- stores 1-bit value.
- **reset-set latch (RS)**
	- two inputs - S and R
	- one output value - Q (value stored in the latch)
	- may also output NOT(Q)
- when both R and S are 1, the value of the latch is stable 
- control circuit controls that R and S are NEVER 0 at the same time
- to store 0, R is set to 0 (S == 1)
- to store 1, S is set to 0 (R == 1)
![[Pasted image 20221109203633.png]]

#### Gated D Latch
- **gated D latch** adds ensures that R and S won't be 0 at the same time.
	- data (D) input - value to be stored
	- write enable (WE) input - controls writing 
		- gated D latch writes only when WE is 1.
![[Pasted image 20221109204430.png]]


#### CPU Register
- by linking multiple 1-bit D latches an N-bit D latch can be made, e.g. 32-bit register.
	- 32-bit data value input
	- 1-bit Write Enable (WE) signal input
![[Pasted image 20221109205235.png]]
- 3-bit gated D latch