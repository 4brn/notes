## Recall
- array -> ordered collection of data of the same type *contiguously* stored in memory.
	- `Type arr[N]` -> `arr` of type `Type` with `N` elements
	- `arr[i]` == `*(arr + i)`, since `arr` is of type `Type` -> `*(arr + i * sizeof(Type))`
		- example in C
```c
void printArr(void* arr, int length, int size, void (*printer)(const void*)){
    for(int i = 0; i < length; i++){
        printer((arr + i * size));
    }
}
```

## Common array operations

- `arr` -> `int arr[10]`
- `%rdx` -> address of `arr`
- `%rcx` -> `i`
- `%rax` -> `x`

|Operation |Type| Assembly Representation
--- | --- | ---|
|x = arr|int*|mov %rdx, %rax
|x = arr[0]|int|mov (%rdx), %eax
|x = arr[i]|int|mov (%rdx, %rcx, 4), %eax
|x = &arr[3]|int*| lea 0xc(%rdx), %rax
|x = arr+3|int*| lea 0xc(%rdx), %rax
|x = \*(arr+5)|int*|mov 0x14(%rdx), %eax
- `mov (%rdx, %rcx, 4), %eax` -> `mov (%rdx{arr} + %rcx{i} * 4{sizeof(int)}), %eax`
- `int` -> 4 bytes 
- `int*` -> 8bytes
![[Pasted image 20221120094647.png]]
- address of element 3 -> `arr + 3 * sizeof(int)` -> `arr + 12`
- follow the [example](https://diveintosystems.org/book/C7-x86_64/arrays.html) from the book
	- `cltq` -> *convert long to quad*, takes the last register/memory address as input
		```r
		mov -0x8(%rbp), %eax 
		cltq # %eax -> %rax
		
		lea  0x0(,%rax,4),%rdx # i*4 + 0x0 -> %rdx
		mov -0x18(%rbp),%rax # copy arr to %rax (arr is just a memory address)
		add %rdx,%rax # add the before calculated offest to arr (arr + i*4)
		mov (%rax),%eax # dereference arr + i * 4 and put it into %eax
		add %eax, -0x4(%rbp) # add result to total 
		# 5 instructions above correspond to: total += array[i]
		```
	- converts value stored in `%eax` to a 64-bit integer that is stored in `%rax`. Needed as the next instruction performs a *pointer arithmetic* and pointers take 8 bytes.