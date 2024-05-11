**resource**([Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence))

## Arithmetic

### +
plus/concatination.

### ++
adds 1.

### - 
minus.

### --
subtracts 1.

### *
multiplication.

### / 
division.

### **
to the power of something (2\*\*3 = 2 to the 3rd = 8).


## Keywords

### typeof

Returns the type of a variable.

## Comparison 

Comparison operatios return *boolean*.

### >
Greather than.

### < 
Smaller  than.

### >=
Grater than or equal.

### <= 
Smaller than or equals.

## Equality

### =
assignment a variable with a value.

### == 
*Loose* equality operator(allows [[Type Coercion]])
- **AVOID BECAUSE OF BUGS**.

### === (Strict equality)
*Strict* equality operator

*exactly equal*(needs to be the same data type).
- returns a *boolean* value (true or false).

### !=
Not equal (*Loose* equality operator)

### !==
Not equal (*Strict* equality operator)

## Logical

### &&
AND

### ||
OR

### !
NOT

## Conditional (Ternary)
```javascript
const age = 23;
age >= 18 ? console.log("I like to drink wine") : console.log("I like to drink water");

OR


const drink = age >= 18 ? 'Wine 🍷' : 'Water 💧'; //this ternary operator returns a EXPRESION(Just a value).
console.log(`I like to dring ${drink}`)
```

### Syntax:
1. Condition
	Starts with the condition (age >= 18).
2. If part
	After the *?* symbol we write the *IF*(true) statement (*1* line only).
3. Else part
	After the *:* symbol we write the *ELSE*(false) statement (*1* line only).



