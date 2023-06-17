A piece of code we can reuse in a program. 

## Function Declaration
```javascript
function name (){
	//code to execute
}
```
We can call declaration functions before they were defined.

### Parameters

Parameters are input data that the function needs to run.
```javascript
function fruitProcessor (apples, oranges){
	console.log(apples, oranges);
	const juice = `Juice with ${apples} apples and ${oranges} oranges.`;
	return juice;
}

const appleJuice = fruitProcessor(5,0); // to store the return of fruitProcessor function we a variable.
```

## Calling/Running/Invoking

After a function has been declared you need to call it to perform its nested code.

```javascript
functionName();
```
### Calling a function within another function

```javascript
function cutFruitPieces(fruit){
	return fruit * 4;
}

function fruitProcessor (apples, oranges){
	
	const applePieces = cutFruitPieces(apples);// called and stored another function
	const orangePieces = cutFruitPieces(oranges);// called and stored another function
	
	const juice = `Juice with ${apples} pieces of apple and ${oranges} pieces of orange.`;
	return juice;
}
```

## Function Expression

Works the same way as Function Declaration
```javascript
//the function is stored within the cariable calAge1 -> Anonymous function(has no name)
const calcAge1 = function(birthYear){ 
	return 2037 - birthYear;
} 

// 
const age2 = calcAge1(1991);
```
Can't be accessed prior to its definition.

calcAge1 will hold the function which in this case is an [[Expressions And Statements#Expressions|expression]].

_In JavaScript functions are expessions._

### Arrow Function

More compact way of writing one line functions(Still an expression).

```javascript
const calcAge3 = birthYear => 2037 - birthYear;

const age3 = calcAge3(1991);
console.log(age3);
```
Arrow functions don't require the return keyword.

#### Multiple Line Arrow Function
```javascript
const yearsUntilRetirement = birthYear => {
	const age = 2037 - birthYear;
	const retirement = 65 - age;
	return retirement;
}

yearsUntilRetirement(1991);
```
To write multiple line arrow functions we need {} as well as the **return** keyword.

#### Multi Parameter Arrow Function

```javascript
const yearsUntilRetirement = (birthYear, firstName) => {
	const age = 2037 - birthYear;
	const retirement = 65 - age;
	return `${firstName} retires in ${retirement} years.`;
}

console.log(yearsUntilRetirement(1991));
```
We need to wrap the parameters in <mark>()</mark>, listing them using <mark>,</mark>.

### Methods

Fuctions inside of [[Objects]] are called **methods**. Methods are expressions.
```javascript
const jonas = {
    firstName: 'Jonas',
    lastName: 'Schmedtmann',
    birthYear: 1991,
    job: 'teacher',
    frients: ['Michael', 'Peter', 'Steven'],
    hasDriversLicense: true,

    calcAge: function() {
        return 2037 - this.birthYear;
    },

    output: function() {
        const message = `${this.firstName} is a ${this.calcAge()}-year old ${this.job}, and he has ${this.hasDriversLicense ? 'a' : 'no'} driver's license`;
        return message;
    }
};

console.log(jonas.output());
```
You need to add () at the end to make it a method, otherwise it sees it a property.