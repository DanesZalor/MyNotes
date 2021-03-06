# PHP intermediate
## Predeined Variables
A **superglobal** is a predefined variable that is always accessible.
PHP's superglobal variables are *$_SERVER, $GLOBALS, $_REQUESTS, $_POST, $_GET, $_FILES, $_ENV, $_COOKIE, $_SESSION*.


|[`$_SERVER`](https://www.w3schools.com/php/php_superglobals_server.asp)|returns|
|-|-|
|`'PHP_SELF'` or<br>`'SCRIPT_NAME'`|file name of currently executing script|
|`'SCRIPT_FILENAME'`|full directory of currently executing script|
|`'SERVER_NAME'`|name of host server|
|`'SERVER_PORT'`|port being used|
|...|...|

## PHP Forms
![php forms](.imgs/phpforms1.png)
`action="submitPage.php"` indicates to use `submitPage.php` when enter is pressed<br>
`method="post"` indicates to use an http POST method

the `$_POST` superglobal array holds the key/value pairs of the `<input>` where their<br>key=**name** and<br> value=*whatever value was inputted*

![php form](.imgs/phpforms1-form.png)

![php formsubmit](.imgs/phpforms1-formsubmit.png)

### GET and POST
are two methods of submitting forms.
Information sent from a form via the **POST** method is invisible to others, since all names and/or values are embedded within the body of the HTTP request.

> there are no limits to the amount of information to be sent.
> It is not possibel to bookmark the page, as submitted values are not visible.

Using the same example above, but changing the method to **GET**
![formGet](.imgs/phpforms1-formGET.png)
![formGetRes](.imgs/phpforms1-formGETRes.png)

> GET should **NEVER** be used for sending sensitive information

## $_SESSION

You can store information in the `$_SESSION` superglobal. It can be used accross multiple pages. Information is stored in the server. By default, session variables last until the user closes the browser. 

use `session_start()` to initiate session
```php
session_start();
```

## Cookies
Cookies are often used to indentify the user. It is a small file that the server embeds on the user's computer. Each time the same computer requests a page through a browser, it will send the cookie too.

```php
setcookie(name, value, expire, path, domain, secure, httponly);
```

|variable||
|-|-|
|name|specifies cookie's name|
|value|specifies cookie's value|
|expire|specifies (in seconds) when the cookie expires.<br>`time() + seconds`<br>`time() + 86400 + days`|
|path|specifies server path of cookie.<br> If set to `/` the cookie will be avaialable within the entire domain.<br> if set to `/php/`, the cookie will only be available within the `php/` directory and all sub-directories of it.|
|domain|specifies cookie's domain name. To make the cookie available on all subdomains of *example.com*, set the domain to `example.com`|
|secure|specifies whether or not the cookie should only be transmitted over secure HTTPS connection.|
|httponly|if set to TRUE, cookie will be accessible only through HTTP protocol.|

> **name** parameter is the only one required.


Example
```php
<?php
$value = "John";
setcookie("user", $value, time() * (86400 * 30), '/' );

if(isset($_COOKIE['user'])){
  echo "Value is: ". $_COOKIE['user'];
}
// outputs "Value is: John";
?>
```
> `setcookie()` must appear BEFORE the `<html>` tag.<br>**Never** store sensitive information in cookies.

## Manipulating Files
`fopen(filename, mode)`

|modes||
|-|-|
|r|opens file for read only|
|w|opens file for write only.<br> Erases the contents of the file or creates a new file if it doesn't exist|
|a|opens file write only|
|x|creates a new file for write only|
|r+|opens a file for read/write|
|w+|opens a file for read/write.<br>Erases the contents of the file or creates a new file if it doesn't exist|
|a+|opens file for read/write. Creates new file if the file doesn't exst|
|x+|creates a new file for read/write|

#### Example - writing to a file
```php
<?php
  $myfile = fopen("names.txt", "w");
  $txt = "John\n";
  fwrite($myfile, $txt);
  $txt = "David\n";
  fwrite($myfile, $txt);
  fclose($myfile);
?>
```

> makes a file called `names.txt` with the context `"John\nDavid\n"`;

#### Example reading a file
`file(filename)` returns the contents of a file in an array where each line is an element
```html
<html>
<head>
    <title>Test-html</title>
</head>
<body>
    <h1> this is a test </h1>
    <p> among many other things</p>
</body>
</html>
```

```php
$myfile = file('test.html');
foreach( $myfile as $line) 
  echo $line;
```
> you can use `count()` method on the array to count the strings

> **Output**<br>![file read res](.imgs/filereadtest.png)

#### Example - appending to a file
```php
$myFile = "test.txt";
$fh = fopen($myFile, 'a');
fwrite($fh, "Some text");
fclose($fh);
```
> this will append `"Some text"` in `test.txt`

