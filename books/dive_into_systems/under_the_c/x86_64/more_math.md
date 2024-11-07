- **load effective address (lea)** - operates on the same operand structure but *doesn't* perform memory lookup (treats addresses as numerical values)
![[Pasted image 20221123091030.png]]
- arithmetic instructions:
![[Pasted image 20221123091105.png]]
- bit shifting -> better performance than multiplication and division, compiler optimizes this process internally
	- `0b0011 << 2` -> `0b1100`
![[Pasted image 20221123091325.png]]
- bitwise instructions -> don't use bitwise instructions in C when it's not needed!!!
![[Pasted image 20221123091404.png]]