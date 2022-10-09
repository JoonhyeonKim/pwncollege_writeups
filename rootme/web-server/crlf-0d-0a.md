# CRLF(%0D%0A)

\r\n: Windows, HTTP \n: Linux

The term CRLF refers to Carriage Return (ASCII 13, \r, 0x0D) Line Feed (ASCII 10, \n, 0x0A). They’re used to note the termination of a line, however, dealt with differently in today’s popular Operating Systems. For example: in Windows both a CR and LF are required to note the end of a line, whereas in Linux/UNIX a LF is only required. In the HTTP protocol, the CR-LF sequence is always used to terminate a line.

A CRLF Injection attack occurs when a user manages to submit a CRLF into an application. This is most commonly done by modifying an HTTP parameter or URL.

***

Then use CRLF (%0D%0A) to do log injection:

http://challenge01.root-me.org/web-serveur/ch14/?username=admin%20authenticated.%0D%0Aguest\&password=guest

\-> in log it will be soted as : admin authenticated. guest failed to authenticate.
