# JavaScript


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


## AJAX Request
Can be asynchronous (executed all at once) or synchronous (executed all at once).

```Javascript
// sending a request to a server
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();

```


# jQuery

## Events
```Javascript

// When inside of an event, you can access the item
// that triggers the event by using $(this).

// The first argument is for the event itself, so (e) or (event)

// click event on ID
$('#myDiv').on('click', function () {
	// you can use $(this) to apply changes to '#myDiv' 
});

// click event on class (applies to all classes)
$('.myDiv').on('click', function () {
	// stuff here
});

// double click event
$('.myDiv').on('dblclick', function() {
	// code here
});

// click keypress event on enter key only when focused
$('input').on("focus", function() {
  $('#div').on('keypress', function() {
	if (event.keycode == 13) {
	// code here
	}
  }
});
	
// run an event before the DOM
$('document').on("click", "#clickedItem", function() {
	// code here
});
	
// targeting an input
$('input[type=radio][name=name]').on('click', function() {
	// code here
});
	
// live search (RegExp match w/ table rows)
$('#searchInput').on('keyup', function(e) {
// value of text field
var value = $(this).val();
var patt = new RegExp(value, "i");
	$('#table-id').find('tr').each(function() {
	var $table = $(this);
		if (!($table.find('td').text().search(patt) >= 0)) {
		$table.not('th').hide();
		}
		if (($table.find('td').text().search(patt) >= 0)) {
		$(this).show();
		}
	});
});
	
	
```

## Loops & Iterators
```Javascript
// loop through each element
$('.myDiv').each(function(index, element) {
	// code here
})

// loop through each 'tr' within #table
$('#table').find('tr').each(function() {
	// code here
})


```

## Load AFTER DOM 
```Javascript

$(function () {
	// this loads AFTER the DOM
});

```

## Load BEFORE DOM
```Javascript

$(window).on("load", function() {
	/// this loads BEFORE the DOM
});

```

## Setting Input Values
```Javascript

$('#inputID').val('newValue');

```

## Changing CSS
```Javascript

// for one class
$('.myClass').css("color", "blue");

// for multiple classes
$('.myClass').css("")

```

## Changing Focus
```Javascript

$('input').focus();

```

## Check if item is checked...
```Javascript
// for instance, to use with an on change event
if ($(this).prop("checked") == true) {
	// do something 
} else {
	// do something}
```