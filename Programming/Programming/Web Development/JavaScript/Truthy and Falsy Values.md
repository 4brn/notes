There are *5* falsy values:
	*0*, *''*, *undefined*, *null*, *NaN*.

```javascript
console.log(Boolean(0)); //prints false
console.log(Boolean(undefined)); //prints false
console.log(Boolean('Jonas')); //prints true
console.log(Boolean({})); //prints true
console.log(Boolean('')); //prints false
```

Could be used when you need variable with a value:
```javascript
const money = 0; //0 is falty value 
if (money) { 
	//money is other than 0
	console.log("dont spend it all");
} else {
	//money is 0 (falsy value)
	console.log("There is no money")
}


let height; // falsy value (undefined)
if(height) {
	//height is defined
	console.log("Yay, height is defined")
} else {
	//height is undefined
	console.log("height is undefined")
}
```