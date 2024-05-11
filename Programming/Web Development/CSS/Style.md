```css
<style> 
	body { // element selector (currently it changes the whole body element.)
		background-color: green;
	}
</style>
```

This is can be written in the *html* file.

Usually CSS is written on an separate file (style.css). 

Look at *Link*:
```html
<link href="style.css" rel="stylesheet" />
```

Used to _link_ the CSS Style file to the HTML file.

## Styling classes

```css
.class-name{

}
```

By using the "." before the name of the class attribute in the *html* file.

## Styling ID's

```css
#id-name{

}
```
By using the "#" before the name of the id attribute in the *html* file


## Styling All elements
```css
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
```

By using "\*" 


## CSS File

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: rgb(255, 247, 201);
  font-family: Arial;
  font-size: 20px;
  padding: 50px;
}

h1 {
  font-size: 35px;
  margin-bottom: 25px;
}

h2 {
  margin-bottom: 20px;
  text-align: center;
}  

p {
  margin-bottom: 20px;
} 

.first {
  color: red;
}

#your-name {
  background-color: rgb(255, 220, 105);
  border: 5px solid #444;
  width: 400px;
  padding: 25px;
  margin-top: 30px;
}

input,

button {
  padding: 10px;
  font-size: 16px;
}

a {
  background-color: yellowgreen;
}

#course-image {
  width: 300px;
}

#your-name h2 { /*targets the h2 element in the tag with the "your-name" id*/
  color: olivedrab;
}
```

