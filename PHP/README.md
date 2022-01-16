# PHP

## Array Manipulation

```php
// here is a foreach loop, a good way to iterate through an array
foreach ($arr as &$value) {
	// stuff here
}

```

## (Prepared) Statements for Queries

Prepared statements work like this:
1. Prepare - an SQL statement template is created and sent to the database. Certain values are left unspecified, called parameters (labeled "?"); 
2. The database parses, compiles and performs the query optimization on the SQL statement template and stores the result without executing it.
3. Execute - at a later time, the application binds the values to the parameters and the database executes the statement. The application may execute the statement as many times as it wants with different values.

**Note:** The question marks are for using prepared statements. Statements only need to be prepared if you are accepting custom inputs from your users.


```php

// INSERT statement
$stmt = $con->prepare("INSERT INTO table(col1, col2) VALUES (?, ?)")

// SELECT statement
$stmt = $con->prepare("SELECT * FROM table WHERE id = ?");

// UPDATE statement
$stmt = $con->prepare("UPDATE table SET col1 = ?, col2 = ?");

// DELETE statement
$stmt = $con->prepare("DELETE FROM table WHERE id = ?");

// the params should match the ?s in your query
// they need to follow the SAME order as they appear in the query
// you can also use variables if you need to filter it first.
$stmt->bind_param("ss", 'columnName1', 'columnName2');

// then you execute
$stmt->execute();

// this gets a result set from a prepared statement
$result = $stmt->get_result();

// if you want to get a count of rows, you can do...
$stmt->store_result();
$match = $stmt->num_rows();


$output = "";

// this loops through the array of the values
while ($row = $result->fetch_assoc()) {
 $Id = $row['id'];
 $Date = $row["dateposted"];
 $Time = $row["timeposted"];
 $Title = $row["title"];
 $Entry = $row["entry"];
	
// protip, the stuff inside 'while' loops through the logic inside
// for every file. sometimes you gotta access that stuff outside
// of the loop. An easy way to do that would be to use:
$id[] = $row['id']; // use this inside of the while loop
	
// any of the above variables can be echoed below to output the result
}
// then, after the while loop, if you use the $id variable,
// it returns an array of all arrays that you can then iterate through
// the best way I've found to display contents of an array is:
$var = implode(",", $description);
 ```
 
 The `bind_params` first value is the argument, which may be one of four types:
 - i - integer
 - d - double
 - s - string
 - b - BLOB

## Error Output

```php

// to enable detailed error reporting, use the following
$driver = new mysqli_driver();
$driver->report_mode = MYSQLI_REPORT_ALL;

// or you can use this for less strict error reporting
$driver->report_mode = MYSQLI_REPORT_ERROR;

$stmt = $con->prepare("SELECT * FROM blogs");

// this checks the database connection and returns if there is an error
if (false === $stmt) {
 die('prepare() failed:' . htmlspecialchars($stmt->error));
 exit();
}

$stmt->bind_param("s", $username);

// this checks if bind_params was successful
if (false === $stmt) {
 die('bind_params() failed:' . htmlspecialchars($stmt->error));
 exit();
}

$stmt->execute();

// checks if execution was successful
if (false === $stmt) {
 die('execute() failed:' . htmlspecialchars($stmt->error));
 exit();
}


```


## Header Redirects

```php
header('location: admin.php');
```

## Sessions

```php

// if a page should only be viewable to someone who is logged in, add this at the top:

// if user is NOT logged in...
// the 'uname' part above should match the variable that is on login.php
if (!isset($_SESSION['uname'])) {
 // redirect them to another page
 header('Location: index.php');
} else {
 // if user IS logged in, do stuff
}



```



## Includes & Requires

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

## Regular Statements 

Some statements don't need to be prepared, such as `SELECT * and COUNT(*)` queries. 

These can be executed like so:

```php

$sql = "SELECT * FROM websites";

if ($result = mysqli_query($con, $sql)) {
	// if there's more than 0 results
	if (mysqli_num_rows($result) > 0) {
		// this part loops
		while ($row = mysqli_fetch_array($result)) {
			$id = $row['id'];
			$url = $row['url'];
			// etc.
		}
	}
}
```

```php

// this selects how many records are in a specific column

$sql = "SELECT COUNT(*) FROM websites WHERE category='personal'";
$qry = mysqli_query($con, $sql);
$personalCount = mysqli_fetch_assoc($qry)['COUNT(*)'];

```

## GET and POST

These methods send encoded user information appended to the page request (the URL). Each of the enocded information are separated by the **?** character, like so:

```
https://sadgrl.online/index.html?var1=value1&var2=value2&var3=val3
```

### GET

This method is restricted to 1024 characters. This method is not meant to be used to send passwords or sensitive information to the server. It also can't be used to send images or files to the server.

```php

$_GET["variable"];

```

### POST

The POST method also sends encoded user information, but does so through HTTP headers. There is no size restriction and if your site is secured with SSL, it is much safer to transfer sensitive information.

```php

$_POST["variable"];

```

## isset()

Before doing logic on a GET/POST action, it's best to wrap it in an isset statement:

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
	
// combining statements:
	
if(isset($_GET['value1']) and isset($_GET['value2']) {
	// stuff here
}
   
// combining and checking if values are NOT empty
if (isset($_GET['value1']) && !empty($_GET['value1']) and isset($_GET['value2']) && !empty($_GET['value2'])) {
	// stuff here
}

```


## Filter Input
```php

$filteredInput = filter_input(INPUT_POST, 'postValue');

// escape slashes
$filteredInput = preg_replace("#^[^:/.]*[:/]+#i", "", $url);

```

## Strip Input

This removes whitespace from the beginning and the end of the string.

```php

$name = trim($_POST['name']);

```


## AJAX with PHP

When you want to transfer GET or POST data from HTML to PHP without a page refresh, it is necessary to use AJAX. In the example below, I submit the ID and "reason" of the item being deleted.

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

## Date and Time

```php

// set the timezone
date_default_timezone_set("US/Eastern");

```


## Sessions

This is the file that every page hidden behind a login screen should reference in order to tell whether a visitor is logged in.

```php

if(!isset($_SESSION["username"])) {
	header("location: https://google.com");
	exit();
}

// I don't know too much about this yet, but I've used it in the past to assign specific 'roles'. For example, I set the token when I log in to "sadness" and anyone whose token does not match, will not be able to see the page.

```

Then, on the pages you want users to have to be logged in to see:

```
include "auth-session.php";
session_start();
```

The sessions will stay active, even after the user logs out. We don't want this to happen so we need to make a `logout.php` with this:

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

 # Notes
- Quotation marks and apostrophes are weird in PHP. Usually when echoing stuff, you want the echo content to be wrapped in double quotes and everything inside to be wrapped in single.