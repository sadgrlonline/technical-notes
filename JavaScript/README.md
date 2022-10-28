# JavaScript

Also see [jQuery](jQuery)

## Table of Contents
- [Selecting and iterating elements](#selecting-and-iterating-elements)
- [DOM manipulation](#dom-manipulation)
- [Random number](#random-number)
- [Array manipulation](#array-manipulation)
- [String Manipulation](#string-manipulation)
- [Loops and Iterators](#loops-and-iterators)
- [Prevent Form Spam](#prevent-form-spam)
- [Objects](#objects)
- [Intervals](#intervals)
- [localStorage](#localstorage)
- [Checking if Mobile Device](#checking-if-viewed-on-mobile-device)
- [Confirmation Dialog](#confirmation-dialog)
- [URL search params](#url-search-params)

## Selecting and iterating elements

```Javascript
// get element by ID
var button = document.getElementById('#button');

// get elements by class:

// METHOD 1: (querySelectorAll)
// (can also be used for element tags)

var items = document.querySelectorAll(".item");
// selects all .item / class="item" elements

// to iterate:
items.forEach((item) => {
   console.log(item);
})

// METHOD 2: (getElementsbyClassName)

var items = document.getElementsByClassName("item");
// selects all .item / class="item" elements

// to iterate:
for (var i = 0; i < items.length; i++) {
   console.log(item[i]); // each item
}
// OR
Array.from(items).forEach((item) => {
   console.log(item); // each item
})

--

// tricks:

// select all checked radio buttons:
document.querySelectorAll('input[type="radio"]:checked');
```
## DOM manipulation

### DOM methods
```Javascript

var div = document.createElement('div'); // create a new element*
// (or select an existing one)
div.setAttribute("id", "myDiv"); // assign unique id
div.removeAttribute("id", "myDiv"); // remove id
div.classList.add("item"); // add class
div.classList.remove("item"); // remove class
if (div.classList.contains("item")) { ... } // check if a class exists
div.innerHTML = `<p>Hello world!</p>`; // add HTML
div.style.color = "blue"; // set/change single-word CSS property
div.style.backgroundColor = "yellow"; // set/change dual-word CSS property
div.style.classList.length; // get number of classes
div.append(el) // attaches after the selected element
div.prepend(el) // attaches before the selected element
document.documentElement.style.setProperty("--bg-color", "#000000"); // change root variable value

// * if creating an element with JS,
// appending the created element to the DOM should come last
// you won't be able to see anything until you append it

// more tricks

// get position of cursor during event:
var rect = e.target.getBoundingClientRect();
var left = rect.left + window.scrollX;
var top = rect.top + window.scrollY;

// automatically resize textarea elements' height
// expand based on content
var textarea = document.querySelectorAll('textarea');
textarea.forEach(function(box) {
    var value = box.value;
    var numLines = value.split(/\r\n|\r|\n/).length;
    box.setAttribute("rows", numLines);
  });
```

### Run after DOM is loaded
```Javascript
document.addEventListener("DOMContentLoaded", function() {
   // code here
}
```

### Event Listeners

#### Attaching event listeners

```Javascript
var button = document.getElementById("button");

// there are two ways you can do this:

// METHOD 1:

button.addEventListener("click", myFunction);
// - runs a function on execution
// - easier to organize (and reuse)code when done this way

// you can access certain information about the event
// by passing an argument
function myFunction(e) {
   console.log("test!");
   console.log(e); // outputs: [object MouseEvent] (but watch this:)
   console.log(e.target); // outputs: <button id="button">Click me</button>
   console.log(e.target.getAttribute("id")); // outputs: "button"
   console.log(e.target.innerText); // outputs: "Click me"
}

// METHOD 2:

button.addEventListener("click", function(e) {
   // all of the above logic regarding "e" applies here
})
```

#### Types of event listeners
```Javascript
// triggered when element is clicked
element.addEventListener("click", myEvent);

// triggered when user hovers cursor over item
element.addEventListener("mouseover", myEvent);

// triggered when item is :focused (useful for input fields)
input.addEventListener("focus", myEvent);

// triggered each time a keystroke is pressed while focused on this element
input.addEventListener("keypress", myEvent); 
// (e.keyCode will give you the code of the key entered. 13 = the enter key.)
```


## Random number
```Javascript
// a random number up to 9
var random = Math.floor(Math.random() * 10);

```

## Array manipulation
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
## URL search params

With JS, it's possible to grab some variable from the URL and use it on the page somehow.

```Javascript
// let's say my website is website.com
// but I want to show someone's name when you enter website.com/?name=Someones+Name

// first, define these variables
const queryString = window.location.search;
const urlParams = newURLSearchParams(queryString);

// then create one for your new parameter
var name = urlParams.get("name");

// check if the parameter exists
if (name) {
   // logic here
}
```
