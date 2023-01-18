```javascript
const day = 'monday';

switch(day){
	case 'monday':
		console.log("Go to English practice");
		break;
	case 'tuesday':
		console.log("Go to BJJ");
		break;
	case 'wednesday':
		console.log("Practice Javascript");
		break;
	case 'thursday':// if there is no break if automatically goes to the next case (could be used as a answer to multiple caser)
	case 'friday':
		console.log("Go to school");
		break;
	case 'saturday':
		console.log("Play videogames");
		break;
	case 'sunday':
		console.log("Get ready for monday");
		break;
	default:
		console.log("Not a valid day")
}
```

If there is *no* break if *automatically* goes to the next case (could be used as a answer to *multiple* cases).