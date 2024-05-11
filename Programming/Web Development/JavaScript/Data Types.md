## Primitive data types

### Number

decimals and integers
```javascript
let age = 23;
```

### String
Sequence of characters
```javascript
let firstName = 'Jonas';
```

### Boolean
Logical type that can be only *true* or *false*.
```javascript
let fullAge = true;
```

### Undefined
Variable that is not yet defined with a value.
```javascript
let children;
```

### Null
Means 'empty value'.

### Symbol(ES2015)
Value that is unique and cannot be changed.

### BigInt(ES2020)
Larger integers the number type can hold.

## Keywords
### typeof
Returns the type of a variable.
```javascript
let flag = false;
console.log(typeof flag); // returns boolean
console.log(typeof "Strint"); // returns string

```

### let
Block-scoped.
Declaring variables that can be changed(*mutated*/*reassigned*) later.
```javascript
let number = 10;
console.log(number);

number = 15;
console.log(number);
```

### const
Declaring variables that cannot be changed later
```javascript
const birthYear = 2006;
birthYear = 1999; //returns a error
```
**const** variables cannot be *unassigned*.
```javascript
const job; //returns a error
```

### var
Function-scoped.
Same as *let*, used in the past (before ES6).