Strict mode helps developers with finding bugs.

```javascript
let hasDriversLicense = false;
const passTest = true;

if(passTest) hasDriverLicense = true; //error
if(hasDriversLicense) console.log('I can drive.'); 
```
The 1st if has a spelling mistake, esensialy making it another variable (hasDriverLicense instad of hasDriver<ins>s</ins>License)


```javascript
const interface = 'Audio'; //SyntaxError -> reserved keyoword
const private = 534; //SyntaxError -> reserved keyword
```