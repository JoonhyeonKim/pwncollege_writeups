# emb52: stdin redirection on a python application, cat | script\#

![stdout redirection(subprocess)](<../.gitbook/assets/image (6) (1) (1).png>)

![stdin redirection,observe the entered '-', for 'cat' to keep being opened. ](<../.gitbook/assets/image (9) (1) (1).png>)

with errors

![](<../.gitbook/assets/image (198).png>)



while here is more canonical way

![](<../.gitbook/assets/image (1).png>)

But it does not work. suggested solution was writing p1.sendline() before the p2=process()
