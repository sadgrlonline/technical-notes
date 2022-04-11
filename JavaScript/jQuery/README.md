# jQuery
Also see [Javascript](https://github.com/sadgrlonline/technical-notes/tree/main/JavaScript)

## Table of Contents
- [AJAX Request](#ajax-request)
- [DOM Events](#dom-events)
- [Loops and Iterators](#loops--iterators)
- [Event Propagation](#event-propagation)
- [Input Values](#input-values)
- [Changing CSS](#changing-css)
- [Changing Focus](#changing-focus)
- [Check if item is checked](#check-if-item-is-checked)
- [Snippets](#snippets)

## AJAX Request
Can be asynchronous (executed all at once) or synchronous (executed all at once).

```Javascript
// sending a request to a server
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();

```

## DOM Events
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

## Event Propagation

### Load AFTER DOM 
```Javascript

$(function () {
	// this loads AFTER the DOM
});

```

### Load BEFORE DOM
```Javascript

$(window).on("load", function() {
	/// this loads BEFORE the DOM
});

```

## Input Values
```Javascript

// to set value
$('#inputID').val('newValue');

// to get value
$('#inputID').val()

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
## Snippets

```JS
// I finally figured out how to nicely and easily repopulate an 'edit view' with JS, from a php database (at least in a table form).
        $('.editBtn').on("click", function() {
            // grab the ID of the row being edited
            var id = $(this).parent('td').parent('tr').attr('id');
            
            // grab the length of how many columns (in this case 6)
            //$(this).parent('td').parent('tr').children().length;
            
            // this nicely grabs the existing text inside the cells
            // so we wanna hold onto this and add it to an array
            var dataArr = [];
            $($(this).parent('td').parent('tr').children()).each(function() {
               //console.log($(this).text().trim());
               dataArr.push($(this).text().trim());
            });
            
            // then we loop through again
            i = 0; // using this to keep track
            $($(this).parent('td').parent('tr').children()).each(function() {
               //console.log($(this).text().trim());
               
               $(this).html('<input type="text" value=' + dataArr[i] + '>');
               i++;
               //dataArr.push($(this).text().trim());
            });
        });
```
