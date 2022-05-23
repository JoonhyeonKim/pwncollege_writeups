# emb93: ps > fifo1 | bash command < fifo1 > fifo2 | ps fifo2

![stdin redirection required again](<../.gitbook/assets/image (64).png>)

![Also stdout redirected from the challenge](<../.gitbook/assets/image (182).png>)

![Okay, I got stuck. Maybe I need to make it as an interactive??](<../.gitbook/assets/image (41).png>)

![Yes. I use cat instead of echo to mend.](<../.gitbook/assets/image (107).png>)

Since my script was /challenge/embryoio\_level93 < test

if I type whole stuff in command line, cat > test | bash /challenge/embryoio\_level93 < test > test1 | cat test1. Meaning challenge binary got stdin from test while passed stdout to test1
