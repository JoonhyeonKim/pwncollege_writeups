# Backup file(ffuf)

At first it was just normal login page -> such that I tried to do sqli with ' with no avail -> ran out of idea -> http://challenge01.root-me.org/web-serveur/ch11/index.php\~ -> I get the backup file -> so the file\_name with special character might lead to backup file?? -> URL:PORT/FILECHAR ffuf -u "target" -w "port.txt:PORT" -w "common\_php\_file\_name:FILE" -w "special\_char.txt:CHAR" for usage
