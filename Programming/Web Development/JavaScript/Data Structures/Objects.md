## Object Literal

Literally writing down the entire object content.
```javascript
const jonas = {
	firstName: 'Jonas',
	lastName: 'Schedtman',
	age: 2037 - 1991,
	job: 'teacher',
	frientds: ['Michael', 'Peter', 'Steven']
};
console.log(jonas);// prints everything (alphabetically).
```
The Jonas object has 5 **properties**.

## Getting a property out of an object

Both the Dot and Bracket notations do the same thing

### Dot Notation
```javascript
console.log(objectName.propertyName);
```
### Bracket Notation
```javascript
console.log(objectName['propertyName']);
```
The name of the property should be specified (have a same name as the property)

```javascript
const nameKey = 'Name';
console.log(jonas['first' + nameKey]);
console.log(jonas['last' + nameKey]);
```
In the brackets we can enter any expression:
 ```javascript 
 const interestedIn(`Choose what is jonas interested in`)
```