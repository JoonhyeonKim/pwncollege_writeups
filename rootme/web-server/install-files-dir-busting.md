# Install files(dir-busting)

There was blank page. And I tried few things with no avail.

\->

while I discovered this: directory traversal http://challenge01.root-me.org/web-serveur/../ it gives me the entire web server challenges which I do not know is intended

\->

But thinking it is probably having nothing to do with this challenge, I tried something else.

\->

phpbb is a CMS(content management system http://challenge01.root-me.org/web-serveur/ch6/phpbb/

\->

gobuster dir --url challenge01.root-me.org/web-serveur/ch6/phpbb/ --wordlist /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -t 40

then I found: /install

\->

But it turns out if I brute-force the directory, seems like I got blocked from the site itself for a minute

\->

After I had gotten freed from the ban, I went to that directory, read the install.php
