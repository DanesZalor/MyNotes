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

You can store information in the `$_SESSION` superglobal. It can be used accross multiple pages. Information is stored in the server. By default, session variables last until the user closes the browser. Let's say we have these files:

**index.php**
```html
<html>
<head>
  <title>WebsiteName - Login</title>
</head>
<body>
  <form action="basepage.php" method="post">
    <p>NAME: <input type="text" name="name"></p>
    <p>AGE: <input type="text" name="age"></p>
    <p><input type="submit" name="submit" value="Submit"/></p>
  </form>
</body>
</html>
```
**basepage.php**
```php
<?php
    session_start();
    if($_SERVER['REQUEST_METHOD'] == "POST"){
        $_SESSION['name'] = $_POST['name'];
        $_SESSION['age'] = $_POST['age'];
    }
?>
<html>
<head> <title>WebsiteName</title> </head>
<body>
    <h1>Welcome to WebsiteName</h1>
    <a href="profile.php">Profile</a>
    <p>
    <?php
        echo "Welcome ".$_SESSION['name'].
        "! your age is: ".$_SESSION['age'];
    ?>
    </p>
</body>
</html>
```
**profile.php**
```php
<?php session_start(); ?>
<html>
<head><title>WebsiteName</title></head>
<body>
    <h1>Profile</h1>
    <div> Name: <?php echo $_SESSION['name']; ?> </div>
    <div> Age: <?php echo $_SESSION['age']; ?> </div>

    <a href="basepage.php"> HOME </a>
</body>

</html>
```

|state|screen|
|-|-|
|Upon accessing the server, the `index.html` is loaded. |![sessionTestIndexPage](.imgs/phpSessionTest-indexpage.png)|
|When we submit the form, `basepage.php` is loaded<br>with an http POST request. The session is started and<br> since a POST request is sent, the `$_SESSION` variables<br> are set equal to the `$_POST` variable counterpart. |![sessionTestBasePage](.imgs/phpSessionTest-basepage.png)|
|if we click the *Profile* hyperlink, it redirects us to<br>`profile.php`.The session is started so the<br> `$_SESSION` data is loaded.|![sessionTestProfilePage](.imgs/phpSessionTest-profilepage.png)|
|If we click the *HOME* hyperlink, it redirects us to<br>`basepage.php`. Since it's not a POST request,<br> the `$_SESSION` data is not reassigned and the page<br> displays the same information.|![sessionTestBasePage2](.imgs/phpSessionTest-basepage.png)|

> Resource: [w3schools](https://www.w3schools.com/php/php_sessions.asp)