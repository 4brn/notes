
## Declaration
```javascript
const arr = [1991, 1984, 2008, 2020];
```
OR
```javascript
const years = new Array(1991, 1984, 2008, 2020);
```
## Extraction 
```javascript
console.log(years[0]); // this gives us the value of the 1st (index 0) element -> 1991
```
### length

`arrayName.length` - returns the number of elements in the array.

## Array Methods

### .push()
Adds a element to the end of an array.
```javascript
years.push(2030); // adds 2030 after the last element (2020)
```
.push() could also return the length of the new array.
```javascript
const newLength = years.push(2030); // newLenght = 5
console.log(newLength); //prints out 5
```
### .unshift()
Adds a element to the beggining of an array
```javascript
years.unshift(1990); // adds 1990 to the beggining of the array
```
.push could also return the length of the new array

### .shift()
Removes the first element of an array
```javascript
arrayName.shift();// removes the first element of the array
```
.shift() returns the value of the removed element (you could store it in a variable);

### .pop()
removes the last element on an array
```javascript
arrayName.pop(); //removes the last element in the array
```
There is no need for a parameter.

- *.pop() returns the removes element*
```javascript
const popped = arrayName.pop(); // popped stores the .pop() value.
```

### .indexOf()
Returns the index of element in an array.
```javascript
console.log(arrayName.indexOf(value)); //returns the index of value in the array OR -1 if there is no such value. 
```
### .includes()
Returns true of false if the element is in the array
```javascript
console.log(arrayName.includes(someElement));//returts true or false whether someElement is in the array or not
```
NB! - .includes() uses [[Operators#Equality#=== (Strict equality)|Strict equality]] to check.

