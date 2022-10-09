# PHP - Command injection

I get the ping command box for input then classically this one's source would have been like this

ping -c 3 input

such that

; (cmd)

would give you access to system

then

; ls ; ls -la ; cat .paswd ; cat /etc/passwd

***

; | ' \` for checking command injection
