# Free-Space Managment

- notes for [this](https://pages.cs.wisc.edu/~remzi/OSTEP/vm-freespace.pdf) additional resource from the book. (p.148).

## Free-space managment
- Gets hard when the spce consists of variable-sized units -> *external fragmentation*.
- No free *contiguous* space may lead to failing requests for memory.
 ![[Pasted image 20221022161108.png]]
- A request for 15 bytes will fail even though there are 20 free
- when freeing memory using `void free(void *ptr)` the user *doesn't* specify how much memory should be freed.

### Assumptions
- The space where that memory is stored is called *heap* and the structure that is used to manage free space is a *free list*.
	- contains references to all *free chunks* of space.
- *internal fragmentation* -> if an allocater hands out chunks of memory bigger than the requested.
- memory cannot be relocated once handed to the client.

### low-level Mechanisms

#### Splitting
![[Pasted image 20221022162209.png]]
- the free list
- If a request comes for `1 byte` the allocator would *split* one of the two chunks and split it into 2: 1st chunk will return to the caller, the 2nd will remain on the list.
![[Pasted image 20221022162427.png]]

#### coalescing
- refering to the first example, we free the 10 bytes leaving us with 3 chunks of 10 bytes each thus if a user wants 15 bytes it will return *NULL*.
![[Pasted image 20221022162707.png]]
- *coalescing* looks if the freed chunk is next to another free chunk. If so it merges them together, leaving us with a chonky 30 byte chunk.
![[Pasted image 20221022162921.png]]



### Tracking The Size Of Allocated Regions
- the interface `free(void *ptr)*` doesn't take a size parameter, to accomplish accurate "freeing" of memory most allocators use a *header block* which stores the size of the allocated region. 
![[Pasted image 20221022163458.png]]


### Embedding A Free List
- we have 4096-byte chunk of memory to manage (heap == 4KB).
- the list sould be initialized with 1 entry of size 4096 - `header size` .
```c
typedef struct __node_t {
	int              size;
	struxt __node_t *next;
} node_t;
``` 
- initialize the heap
```c

node_t *head = mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_ANON|MAP_PRIVATE, -1, 0);
head->size = 4096 - sizeof(node_t);
head->next = NULL;
```
![[Pasted image 20221022164314.png]]
- a request of 100 bytes comes
 ![[Pasted image 20221022164427.png]]
- if some data is added and then removed, at some point we will get some free chunks of memory. When this happens we *coalesce* the list.

### Growing The Heap
- most traditional allocators start with a small heap and request for more memory from the OS when needed.
- for all examples headers and other details are ingnored and the illustration bellow is used with a `15 bytes` request.
![[Pasted image 20221022165856.png]]
 
#### BEST fit
1. search through the list for chunks as big or bigger than the requested
2. return the smallest in that group (the *best fit*)
- reduces wasted space
- heavy *performence* penalty when performing an exhaustive search
##### Example
- by lokking for the smallest chunk bigger than the request (15) it splits the 20 bytes chunk.
![[Pasted image 20221022170501.png]]

#### worst fit
- quite bad most of the time
- searches for the *biggest* instead of the *smallest* chunk and returns it
- performance...
##### Example
- by looking for the biggest chunk it splits the 30 bytes one
![[Pasted image 20221022170527.png]]

#### First fit
- returns the first chunk that satisfies the request.
- really fast
- pollutes the beginning of the list
- use *address-based ordering* by keeping the list ordered by the address of the free space
	- coalescing becomes easier
	- fragmentation tends to be reduced
##### Example
- selects the same as the *worst search* but faster as it selects the first free one.

#### NEXT fit
- "*next fit* algorithm keeps an extra pointer to the location within the  
list where one was looking last."
- similar to *best fit*, quite slow as well

### Other approaches
- there are a lot more techniques and algorithms to improve memory allocation

#### Segregated lists
- if an application has one or more common requests (with the same size), keep a separate list just for them.
	- good as fragmentation is much less of a concern
- problem -> what size should be the separate list compared to the main one?
	- the *slab allocator* by uber-engineer Jeff Bonwick solves this issue.
	- when the kernal boots, it allocates a number of *object caches* for frequently requested objects (locks, file-system inodes, etc)
	- when running low on memory it requests *slabs* from a more general memory allocator.
	- general allocator can later reclaim the slabs

> Jeff Bonwick was the lead of the ZFS file system


### Buddy Allocation
- *binary buddt allocator* -> main idea is to simplify *coalescing*
- memory is thought of as one big space of size *2^n*
	- when a request is made, space is *recurslively* divided until a block big enough is found (and the next one is too small). Can assossiate the idea with *best fit*.
		![[Pasted image 20221023112730.png]] 
	- sufferes from *internal fragmentation* as it can give only space which is power of 2.
	- when memory is freed, the allocator checks if the *buddy* of that chunk is free. If it is it coalesces the two blocks.
### Other ideas
- main problem -> lack of scaling (searching can get pretty slow)
- 