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