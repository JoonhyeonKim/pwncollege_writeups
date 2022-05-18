# 🟢 emb69: Make own interpreter for shell script \#

This challenge was very tricky one.

![](<../.gitbook/assets/image (239).png>)

Since it requests you to run bash script, but without any argument. Thus argc==0. However shell script itself is taken as an arg\[0]. So normally there's no way argc == 0. However

![](<../.gitbook/assets/image (19).png>)

As it is true that by patchelf you can change interpreter and here, if you name a bin as bash then it can be executed.&#x20;

![](<../.gitbook/assets/image (164).png>)

So I get the flag.
