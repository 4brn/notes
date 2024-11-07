- Structs are used to represent a complex structure of data. 



```c

#include <stdio.h>
#include <string.h>

struct studentT{
	char name[64];
	int age;
	float gpa;
	int grad_year;
};

typedef struct studentT Student;

int checkID(Student s1, int min_age);
void changeName(char* old, char* new);

int main(){
	int can_vote;
	
	Student std1 = {name: "mike", age: 21, gpa: 3.6, grad_year: 10};
	Student std2 = {name: "patrick", age: 9, gpa: 1.6, grad_year: 100};
	
	Student classroom[2];
	classroom[0] = std1;
	classroom[1] = std2;
	
	for(int i = 0; i < 2; i++){
		printf("Students name: %s\n", classroom[i].name);
		printf("Can drink? -> %s\n", checkID(classroom[i], 18) ? "yep" : "nope");
	}
	return 0;
}

int checkID(Student s1, int min_age){
	return s1.age >= min_age;
}

void changeName(char* old, char* new){
	strcpy(old, new);
}

```