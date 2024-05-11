## Document Object Model
Structured representation of HTML documents.
Allows JavaScript to access HTML elements and styles to manipulate them.

Simple Version: An exact representation of an HTML file in JavaScript; HTML and DOM are synced-> can be manipulated.

- can change text
- can change HTML attributes
- can change CSS styles

## DOM Tree

![[Pasted image 20230103082230.png]]

## DOM !== JavaScript
DOM is a part of Web APIs(Google, Mozilla,...) that we can access with JavaScript.

## DOM Manipulation
Using JavaScript we can modify what is shown on the webpage.

### document

#### .querySelector()
A method of document
```javascript
document.querySelector('.classOfElement')
```
Selects an element by based on classes`.message; .button; .randomElementClass; ...`

NB! -> it selects the whole html element: `<p class="message"> Start guessing... </p> // An example`

##### .textContent
Gets the text content of an element.
```html
`<p class="message"> Start guessing... </p> <!-- Declaration of a <p> element --!>
```
```javascript
console.log(document.querySelector('.message').textContent); // Prints out the text content of the DOM element with the ".message" class  -> "Start guessing..."
```
```javascript
document.querySelector('.message').textContent = "Some string!" // Sets the text content of the DOM element with the ".message" class to "Some string";
```
