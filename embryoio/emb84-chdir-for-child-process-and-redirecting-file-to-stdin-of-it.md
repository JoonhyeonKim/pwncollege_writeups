# emb84: chdir for child process and redirecting file to stdin of it

![I should redirect certain file to stdin of challenge binary](<../.gitbook/assets/image (110).png>)

![Then might I use 72nd's source code?](<../.gitbook/assets/image (227).png>)

![Now it is a working directory that I need to change ](<../.gitbook/assets/image (133).png>)

So file I need to redirect is 'kzhtyo' while working directory of challenge should be /tmp/kliule

Which means parent must execute my binary in my home directory while child should be executed in /tmp/kliule and receive its stdin file from the /tmp/kliule/ thus.

![](<../.gitbook/assets/image (20).png>)
