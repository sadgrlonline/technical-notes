# PHP

## Table of Contents
- [Array Manipulation](#array-manipulation)
- [Common Functions](#common-functions)
- [Header Redirects](#header-redirects)
- [Include & Require](#include--require)
- [GET and POST](#get-and-post)
- [isset()](#isset)
- [Strip Input](#strip-input)
- [Date & Time](#date-and-time)
- [Sessions](#sessions)
- [mail()](#using-mail)
- [AJAX with PHP](#ajax-with-php)
- [Passing arrays from PHP to JS](#passing-arrays-from-php-to-javascript)
- [Code Snippets](#code-snippets)




## Array Manipulation

```php
// here is a foreach loop, a good way to iterate through an array
foreach ($arr as &$value) {
	// stuff here
}

```

## Common Functions

```php
// check if a field is empty
if (empty($a)) {
	// do something
}

// display contents of array
$var = implode(",", $array);
echo $var;

```

## Header Redirects

```php
header('location: admin.php');
```

## Include & Require

The `include()` and `require()` statement allow you to include the code contained in a PHP file within another PHP file. Including a file produces the same result as copying the script from the file specified and pasted into the location where it is called.

```php

// include
include "config.php";
	
// require
require "config.php";
```

Typically the `require()` statement operates like `include()`.

The only difference is — the `include()` statement will only generate a PHP warning but allow script execution to continue if the file to be included can't be found, whereas the `require()` statement will generate a fatal error and stops the script execution.

If you accidentally include the same file (typically functions or classes files) more than one time within your code using the include or require statements, it may cause conflicts. To prevent this situation, PHP provides `include_once` and `require_once statements`. These statements behave in the same way as include and require statements with one exception.

The `include_once` and `require_once` statements will only include the file once even if asked to include it a second time i.e. if the specified file has already been included in a previous statement, the file is not included again.

## GET and POST

These methods send encoded user information appended to the page request (the URL). Each of the enocded information are separated by the **?** character, like so:

```
https://sadgrl.online/index.html?var1=value1&var2=value2&var3=val3
```

### GET

This method is restricted to 1024 characters. This method is not meant to be used to send passwords or sensitive information to the server. It also can't be used to send images or files to the server. Using a GET request includes data appended to the URL.

```php

$_GET["variable"];

```

#### Using GET to conditionally display a post on a page
This part is a mouthful but I need to get this down somewhere so I remember it lol. So what if you have a blog app and you want to make a 'view.php' page that shows a specific blog post when a 'view post' link is clicked? 

```php

// the view link would look like this:
echo '<a href="view.php?entry="' . $id . '"id="view">'
// in regular html this would look like <a href="view.php?entry="1" id="view"> if the entry ID was 1.
// the key here is the "entry" value, this is how we will interpret the action from the PHP side
	
// then, view.php would look like this:
	
// if the page sees the 'entry' argument
if (isset($_GET['entry'])) {	
	$id = $_GET['entry']; // this variable holds the id number we just passed 
	$stmt = $con->prepare("SELECT * FROM table WHERE id = ?");
	$stmt->bind_param("s", $id);
	$stmt->execute();
	$result = $stmt->get_result();
		while ($row = $result->fetch_assoc()) {
			// code here
		}
	// more code can be added here
}

```

### POST

The POST method also sends encoded user information, but does so through HTTP headers. There is no size restriction and if your site is secured with SSL, it is much safer to transfer sensitive information.

To POST variables from form fields:

```html
<form method="POST" action="page.php">
	...
</form>
```

PHP uses the **name=""** attribute of form fields to pass field data.

To retrieve the variable, use this code on the "action" page listed above.: 
```php

$_POST["variable"];

```

## isset()

This is used to check for a value, usually a form field value or some variable. The best way I think about this is that it's basically a **trigger** which is only pulled when the **isset()** condition is met.

```php

// this checks if the value 'url' (name of form field) was submitted.
if (isset($_POST['url'])) {
 	$url = $_POST['url'];
 	echo $url;
}

// this checks if a value called 'email' was passed in the URL
if (isset($_GET['email']) {
	$email = $_GET['email'];
	echo $email;
}

```

For example, I can have my delete query and edit query logic on the same page, but these 'isset()' statements determine which code to run.

## Strip Input

This removes whitespace from the beginning and the end of the string.

```php

$name = trim($_POST['name']);

```

## Date and Time

```php

// set the timezone
date_default_timezone_set("US/Eastern");

// get current date (formatted for SQL)
$date = date("Y-m-d");

// get current time (formatted for SQL)
$time = date("Y-m-d H:i:s");

// format date
$formattedDate = date("l, F j Y", strtotime($date));
// outputs Wednesday, March 9 2022

// format time
$formattedTime = date("g:iA", strtotime($time));
// outputs 8:36PM

```


## Sessions

To make a page only available to logged-in users, you must create a session and check for the session variable:

```php
// start session
session_start();
// if user is not logged in
if (!isset($_SESSION["username"])) {
	header("Location: ../login/");
} else {
	// run code
}	
```

If have a public page where you want to conditionally show data depending on the session status, you'll also have to include `session_start()` at the top.

Sessions typically stay active for a while. We don't want this to happen so we need to make a `logout.php` with this:

```php
session_start();
session_destroy();
header('location: index.php');
```

## Using mail()

```php
	
        $email = "sadgrl.online@gmail.com"; // specify address
        $to = $email; // send email to our user
        $subject = 'New Yesterweb Ring Application'; // subject
        $message = '

        Someone has recently submitted an application to join the webring. To view pending applications, click <a href="https://miau.sadgrl.online/yesterweb-ring/milkaroni/dashboard/approve/">here</a>.
        
        ';

        $headers = 'From:noreply@sadgrl.leprd.space' . "\r\n"; // this sets the email header's 'from' address
        $headers .= 'MIME-Version: 1.0' . "\r\n";
        $headers .= 'Content-type: text/html; charset=iso-8859-1' . "\r\n";

		// this executes the message send
        mail($to, $subject, $message, $headers);
```


## AJAX with PHP

When you want to transfer GET or POST data from HTML to PHP without a page refresh, it is necessary to use AJAX. In the example below, I submit the ID and "reason" of the item being deleted.

P.S. AJAX requires jQuery :)

### POST

```javascript

$(function() {
	var reason = [];

$('.flag').click(function(e) {
	e.preventDefault();
	$('#submitFlag').click(function(e) {
		// grabbing value to send to PHP
		reason = $(this).siblings('#flagReason').val();
		$this.parents('td').siblings('.flagged').text('⚠️');
		$(this).siblings('#flagReason').val('');
		$(this).parents('#flagReasonDiv').css("display", "none");
			$.ajax({
			type: 'post',
			data: {'id':id, 'reason':reason},
			url: 'index.php',
			success: function(response) {
				//console.log($(this).text());
			}
		});
	});
});
```

Here is how I would grab those values from the PHP end:

```php

// check if ID was POSTed.
if (isset($_POST['id'])) {
    $id = $_POST['id'];
    $reason = $_POST['reason'];
	// more logic here
}

```

### GET

```js

 $(function() {
	 // click handler
 	$('.del').click(function(e) {
		// prevent reload
		e.preventDefault();
		var id = $(this).attr("data-id");
			$.ajax({
				type: 'get',
				url: '?del=' + id,
				success: function(response) {
				$('#' + id).hide();
				}
			});
 		});
 	});
 });

```

Associated PHP:

```php

if (isset($_GET['id'])) {
    $id = $_GET['id'];
	// more logic here
}

```


## Passing arrays from PHP to Javascript
```PHP
// define the arrays first
$idarray = [];
$urlarray = [];
$catarray = [];

while ($row = $result->fetch_assoc()) {

// the [] at the end tells it that it is an array
$idarray[] = $row['id'];
$urlarray[] = $row['url'];
$catarray[] = $row['category'];
	
}
```

```Javascript
// (on same page as above...)
var idArr = <?php echo json_encode($idarray); ?>;
var urlArr = <?php echo json_encode($urlarray); ?>;
var catArr = <?php echo json_encode($catarray); ?>;
// now our database values are available in JS!
```

## Generate a JSON file from Data
```php

    $rows = array();
    $sql = ("SELECT * FROM table");
// the below example only edits a file that already exists
if ($result = mysqli_query($con, $sql)) {
    if (mysqli_num_rows($result) > 0) {
        while ($row = mysqli_fetch_assoc($result)) {
            $rows[] = $row;
        }
    $f = fopen('../file.json', 'w'); // the w means write
    fwrite($f, json_encode($rows));
    }

```

# Notes
- Quotation marks and apostrophes are weird in PHP. Usually when echoing stuff, you want the echo content to be wrapped in double quotes and everything inside to be wrapped in single.

# Code Snippets
For easy copy & pasting

## MySQL Prepared Statements

```php
// SELECT
	$stmt = $con->prepare("SELECT * FROM websites WHERE pending = 0 ORDER BY rand()");
	$stmt->execute();
    $result = $stmt->get_result();
	while ($row = $result->fetch_assoc()) {
		// do stuff
	}
	$stmt->close();

// UPDATE
 	$stmt = $con->prepare("UPDATE websites SET title = ?, url = ?, descr = ?, category = ? WHERE id = ?");
  	$stmt->bind_param("sssss", $title, $url, $descr, $cat, $id);
  	$stmt->execute();
  	$result = $stmt->get_result();
  	$stmt->close();

// CREATE
	$stmt = $con->prepare("INSERT INTO websites(title, url, descr, category) VALUES (?,?,?,?)");
    $stmt->bind_param("ssss", $title, $url, $descr, $cat);
    $stmt->execute();
    $stmt->close();

// DELETE
	$stmt = $con->prepare("DELETE FROM websites WHERE id = ?");
	$stmt->bind_param("s", $id);
	$stmt->execute();
	$stmt->close();

// CHECK IF QUERY HAS MATCHES
	$result = $stmt->get_result();
	$stmt->store_result();
	if(mysqli_num_rows($result) < 1) {
		// if no matches, do this stuff
	}
```
```php
// GET # OF ITEMS FROM COLUMN IN DB
	$number = mysqli_num_rows($result);
```

