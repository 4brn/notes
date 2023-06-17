## Concatination

```javascript
const firstName = "Jonas";
const job = "teacher";
const birthYear = 1991;
const now = 2037;

const message = "I'm " + firstName + ', a ' + (now - birthYear) + " years old " + job + "!";

console.log(message);
```

### Template literals

Write strings in a normal way (easy concatination)

```javascript
const newMessage = `I'm ${firstName}, a ${now - birthYear} year old ${job}`;

console.log(newMessage); // prints out "I'm Jonas, a 46 years old teacher!".

```

Could be used to write *normal* strings.
```javascript
console.log(`Just a simpler Template literal string`);
```

Can make multi-line strings
```javascript
console.log(`String wiht
			multiple
			lines.`);
```