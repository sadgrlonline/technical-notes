# PHP

## Prepared Statements for Queries

Prepared statements work like this:
1. Prepare - an SQL statement template is created and sent to the database. Certain values are left unspecified, called parameters (labeled "?"); 
2. The database parses, compiles and performs the query optimization on the SQL statement template and stores the result without executing it.
3. Execute - at a later time, the application binds the values to the parameters and the database executes the statement. The application may execute the statement as many times as it wants with different values.


```php

// SELECT statement
$stmt = $con->prepare("SELECT * FROM blogs WHERE bowner=?");

// alternatively you can use an INSERT statement
$stmt = $con->prepare("INSERT INTO blogs(bowner, dateposted, timeposted, title, entry) values(?,?,?,?,?)");

// or even an UPDATE statement
$stmt = $con->prepare("UPDATE Applicant SET phone_number=?, street_name=?, city=?, county=?, zip_code=?, day_date=?, month_date=?, year_date=? WHERE account_id=?");

// the params should match the ?s in your query
$stmt->bind_param("s", $username);

// after binding the params, you can set the variables before executing like this:
$username = 'sadness';

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
	
// any of the above variables can be echoed below to output the result
}
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

# Regular Statements 

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

# isset()

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



```

# Passing Variables via a URL

You can add variables to the end of a URL, which helps pass them to another page. For example, if I want to link my 'delete' button to logic, I'll add this code inside of a 'while' loop that outputs each row of my table:

```php

echo "<td> <a href='index.php?del=" . $row['id'] . "'>x</a></td>";

```

This tells the database the user is deleting the row that corresponds with its unique ID. In this way the delete button 'syncs' with the database. 

 # Notes
- Quotation marks and apostrophes are weird in PHP. Usually when echoing stuff, you want the echo content to be wrapped in double quotes and everything inside to be wrapped in single.


# AJAX with PHP

When you want to transfer GET or POST data from HTML to PHP without a page refresh, it is necessary to use AJAX. In the example below, I submit the ID of the item being deleted.

```javascript

// first, I wrap everything in $(document).ready(function() { }) so it runs when the page is fully loaded.
 $(document).ready(function() {
	 // then I have my click event on items with the 'del' class
 	$('.del').click(function(e) {
		// this prevents the form from submitting naturally; make sure you also have no "POST" or "GET" methods in your form tag.
 		e.preventDefault();
		// I needed to pass the unique id to a data attribute, so I used data-id for this. This way, when the HTML and PHP is rendered, every item is created with a data-id that matches their id in the database.
 		var id = $(this).attr("data-id");
		// still inside of the click handler we call our ajax function
 		$.ajax({
		// we want to POST the data
 			type: 'post',
		// this appends our current URL with ?del= and the ID, like this: ?del=1
 			url: '?del=' + id,

 			success: function(response) {
		// when the ajax function completes, the page hasn't reloaded, so while the item is gone from the database, it still appears on the page. To fix this, I also used the db ids to assign an id to each tr (table row) which contains the full entry.
 				$('#' + id).hide();
 			}
 		});
 	})
 });

```

# Quick Snippets
## AJAX POST/GET

```javascript

 $(document).ready(function() {
	 // click handler
 	$('.del').click(function(e) {
		// prevent reload
		e.preventDefault();
		var id = $(this).attr("data-id");
		$.ajax({
			type: 'post',
			url: '?del=' + id,
			success: function(response) {
			$('#' + id).hide();
			}
 		});
 	})
 });

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