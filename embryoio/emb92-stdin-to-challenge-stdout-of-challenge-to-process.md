# emb92: stdin to challenge, stdout of challenge to process

![I need to redirect fifo to stdin of challenge](<../.gitbook/assets/image (165).png>)

![now I need to redirect challenge's stdout ](<../.gitbook/assets/image (99).png>)

![I took the stdin as a 1st fifo and then redirect stdout as 2nd fifo and catching it with cat ](<../.gitbook/assets/image (80).png>)

where script.sh has

\#! /bin/sh

/challenge/embryoio\_level92 < test

![Now with the demanded password, I get the flag.](<../.gitbook/assets/image (66).png>)
