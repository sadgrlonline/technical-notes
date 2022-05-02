# JavaScript

Also see [jQuery](jQuery)

## Table of Contents
- [DOM Manipulation](#dom-manipulation)
- [Random Number](#random-number)
- [Array Manipulation](#array-manipulation)
- [String Manipulation](#string-manipulation)
- [Loops and Iterators](#loops-and-iterators)
- [Prevent Form Spam](#prevent-form-spam)
- [Objects](#objects)
- [Intervals](#intervals)
- [localStorage](#localstorage)
- [Checking if Mobile Device](#checking-if-viewed-on-mobile-device)
- [Confirmation Dialog](#confirmation-dialog)

## DOM Manipulation
Note: DOM manipulation is much more easily done with jQuery.

### Selecting elements by class and ID

```Javascript
// get element by ID
var button = document.getElementById('#button');

// get elements by className:
// this returns a collection of all of the results, which you can iterate through
var myClasses = document.getElementsByClassName("className"); 

// just as a sidenote, I hate iterating through classes with vanilla JS - it's so much easier for non-programmers to understand with jQuery first, tbh.

```

### Run after DOM is loaded
```Javascript
document.addEventListener("DOMContentLoaded", function() {
	// code here
}
```

### Event Listeners
```Javascript
// click listener -> run function
item.addEventListener("click", function);

```


## Random number
```Javascript
// a random number up to 9
var random = Math.floor(Math.random() * 10);

```

## Array Manipulation
```Javascript

// remove last item from array
array.pop();

// remove first item from array
array.shift();

// join arrays into string
array.join();
array.join('-'); // can use a separator in an argument to add one between each item

// map two arrays into a key/value pair - arr1 is the key and arr2 is the value
arr2.map(function(obj, index) {
	var myobj = {};
	myobj[arr1[index]] = obj;
	return myobj;
 });

// combine two or more arrays into a single array
var myCombinedArr = [...arrOne, ...arrTwo, ...arrThree]

// alphabetize or order an array
var myAlphabetizedArray = myArr.sort();

// check if array includes a value
if (myArr.includes('word')) {
	// code here
};

// check if array does not include a value
if (!myArr.includes('word')) {
	// code here
};

// shuffle array (reorder)
function shuffle(urlArr) {
	let currentIndex = urlArr.length, randomIndex;

	// while there are items left to shuffle...
	while (currentIndex != 0) {
	// pick a remaining element...
	randomIndex = Math.floor(Math.random() * currentIndex);

	// decrease
	currentIndex--;

	// swap with current element
	[urlArr[currentIndex], urlArr[randomIndex]] = [urlArr[randomIndex], urlArr[currentIndex]];
	}
	return urlArr;
}

// check for duplicate

// array to check against
var sitesArr = arrayToCheck;
// input to verify
var urlInput = document.getElementById('urlInput');
// our dupe note in the form
var dupe = document.getElementById('dupe');

// makes our function run when the input field is modified
urlInput.addEventListener("change", checkIfDupe);


function checkIfDupe() {
        var value = urlInput.value;
	// urlInput is the field we're checking against the array

        // check if array includes a value
    if (sitesArr.includes(value) {
    // this makes our error message display
        dupe.style.display = "block";
        dupe.style.color = "red";
        dupe.style.fontWeight = "bold";
        submitBtn.disabled = true;
    } else {
    // this reenables the submit button if it's not a duplicate
        console.log('no dupe');
        dupe.style.display = "none";
        submitBtn.disabled = false;
    }
}

```

## String Manipulation

```Javascript
var string = "string";

// identify the last character in a string
string.charAt(str.length -1) // returns 'g'

// remove the last character from a string
string.slice(0. -1); // removes 'g'

// check if another string contains the same value
string.includes('string');


```

## Loops and Iterators

```Javascript
// for loop
for (var i = 0; i < items.length; i++) {
 	// stuff here
 }
// forEach iterator
 item.forEach((arrItem, indx) => {
	// stuff here
 });
```

### Prevent Form Spam

```Javascript
var botField = document.getElementById('botField');
var submitBtn = document.getElementById('submit_btn');

// the submit button starts out disabled
submitBtn.disabled = true;

botField.addEventListener("keyup", checkIfBot);


function checkIfBot() {
  var value = botField.value;
  if (value == "website") {
   submitBtn.disabled = false;
}
}

```

## Objects

```Javascript

// here is the syntax of an object
var object = {
	item: "one",
	item2: "two",
	item3: "three"
}

// here is how you access the stored values:

object.item // returns "one"
object.item2 // returns "two"
object.item3 // returns "three"

```


## Intervals

```Javascript
// run a function on an interval (the numbers are milliseconds)
setInterval(function, 1000);

```

## localStorage

LocalStorage allows the browser to remember values from a page. The values are stored in the user's browser cache.

### Setting
```Javascript

// set a single variable value in the memory
localStorage.setItem('itemName', myVar);

// OR

// set an array into the memory
// JSON stringify makes it into a JSON object
localStorage.setItem('arrName', JSON.stringify(myArr));

```

### Getting
```Javascript

// get a single variable value from memory
localStorage.getItem('itemName');

// AND

// get an array from the memory
var newArr = JSON.parse(localStorage.getItem('itemName'));

```

## Checking if viewed on mobile device
```Javascript

// checks if device is mobile
if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
	// run this code
  }
    });

```


## Confirmation Dialog

To make a box appear that allows the user to confirm or deny a change:

```Javascript
confirm("Are you sure you want to make this change?")
```
