# Flash back

**computer's resource can be used remotely by network, network defined by protocol(ftp, http)** where http eventually becomes dominant,

since it is **hyper text transfer protocol -> it simply navigates users to destination(s) that hold what users want(thus multi clients with one server structure is born, no p2p, one program for multiple users meaning certain user can figure out vuln for all)**, while **the functionality can be implemented with javascript** with the help of server that has the program of use

ethernet(data)/ip(link)/tcp(transfer)/http(application)

where the upper layers cannot affect the lower layers

and application layer protocol needs to have **command and flag** for content specification and details for command, where in http those are http verbs and headers

thus OPTIONS verbs can retireive the options for verbs in headers

Analogy: **http verbs<->os commands, http headers<->os commands' flags** ->&#x20;

do options(with receiving headers):&#x20;

if get: use params url based(send url with SE)&#x20;

else if post: use data api based(tamper values)&#x20;

else if put: use revshell upload based(upload shell)



and for post based:

```
json({"a": "B"}, might be serialized) <-> xml(<xml><a>B</a>) : xml interpreter might allow external entity injection(xxe)
-> <xml><!DOCTYPE foo [<!Entity xxe SYSTEM "/etc/passwd">]> <a>&xxe;</a>
```

thus

for get based:

1. forge the url that is normal for the attacker, but malicious for victim(self xss or account binding, token granting)(use iframe with js for automatically access link, link that is granting perm)
2. input based tampering, sqli nosqli ldapi directory\_traversal etc

for post based:

1. send request for what is not belongs to you: request the info about admin, request register the admin level account
2. input based tampering, as above

meaning, get based is either csrf or input tampering while for web hacking, you may bypass some filter by pretending the payload as the part of url by encoding it with some encode format(like url-encode, double-encode)

\-> then, for api end point(tampering json or xml) for no forms, get params post data tampering(then sending weird links with tags)

\-> post data (json, xml) for web using javascript, while programming paradigm is OOP(object oriented programming), thus javascript object notation(json) is used mainly({"a":"b", "c":function(){\}}) then if one knows the program in the backend: can inject function too??

then use proxy to see the flow of http(since http streams fast, sometimes one can miss the sequence. if there's unintelligible string in params, then it might be a token -> such that one should search for what grants that token -> normally it is one step before that token -> then tamper: if there's url -> get param to manipulate and then forge the malicious url. if there's json or xml -> post data for changing the value) with the proper scope

**http verbs(like commands)** for server to understand the clients request, with the aid of **headers(since http is stateless, it specifies the details of commands. like flags)** if the program for requested is written directly by server side language(options -> get,post,put,head,delete): **http verbs<->os commands, http headers<->os commands' flags** in other words, no form tag else, do the api test with proxy(test application logic with)

***

**Access the page**

**Fire the proxy**

**Record the history**

**Study the Flow**

****

if file is shown directly -> directory traversal, lfi if file is somehow processed by param or data -> sqli, command injection

maybe if there are inputs, then you can do directory traversal, open redirect, command injection, sqli all of them??

directory traversal -> lfi&#x20;

open redirect -> rfi



feroxbuster to find the directory&#x20;

options to check the allowed http verbs



you can use GET /endpoint?file=name request as the testing ground for directory traversal and lfi&#x20;



GET /endpoint?file=../../../etc/passwd and **the trailing escaper's number is determined by the result from the feroxbuster**

send feedback functionality for cmd injection&#x20;

since nowadays cmd injection barely happens

***

document.getElementById("").innerHTML for checking and changing values of web elements
