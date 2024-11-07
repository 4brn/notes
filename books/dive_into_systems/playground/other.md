
## Memory allocation

```c
	int size = 5;
	int* nums1 = (int*) malloc(sizeof(int) * size);
	int* nums2 = calloc(size, sizeof(int));
	nums1 = (int*) realloc(nums1, 2*size*sizeof(int));
```
- don't read or write to *unallocated memory*.


## Func pointers

```c
#include <stdio.h>

int add(int a, int b) {
	return a + b;
}

void greet(char* name){
	printf("Hello %s\n", name);
}

int main(){
	int (*p)(int, int) = &add;
	void (*hi) (char*) = greet;	
	
	hi("Peter");
	printf("sum is -> %d\n", p(1,2));
	return 0;
}
```

## Callbacks
```c
#include <stdio.h>

void hi(){
	printf("Hi\n");
}

void greet(void (*ptr)()){
	ptr();
}

int main(){
	greet(hi);
	return 0;
}
```
- usecase -> a sorting functions can accept a `compare` function.

```c

#include <stdio.h>
#include <stdlib.h>

int compare(const void* a, const void* b){
    int A = *((int*)a);
    int B = *((int*)b);

    return A - B;
}

void printArr(int* arr, int size){
    for(int i = 0; i < size; i++){
        printf("arr[%d] -> %d\n",i, *(arr + i));
    }
}

int main(){
   
    int nums[] = {1, 5, 2, 3, 6, 8, 3};
    qsort(nums, 7, sizeof(int), compare);

    printArr(nums, 7);
	return 0;
}
```


```c
#include <stdio.h>

void printNum(const void* el){
    int num = *((int*)el);
    printf("number -> %d\n", num);
}

void printArr(void* arr, int length, int size, void (*printer)(const void*)){
    for(int i = 0; i < length; i++){
        printer((arr + i * size));
    }
}

int main(){
    int length = 5;
    int nums[] = {1, 2, 3, 4, 5};


    printArr(nums, length, sizeof(int), printNum);
}
```
- a generic print array function.
