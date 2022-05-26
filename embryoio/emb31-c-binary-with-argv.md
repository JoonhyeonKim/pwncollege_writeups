# emb31: c binary with argv\[]

![](<../.gitbook/assets/image (221) (1).png>)

then I tried to do most sane way to add argument

![](<../.gitbook/assets/image (209) (1).png>)

But obviously not works, then

{% embed url="https://stackoverflow.com/questions/12076848/how-to-initialize-argv-array-in-c" %}

{% embed url="https://www.delftstack.com/howto/c/argv-in-c" %}

or this one?

{% embed url="https://stackoverflow.com/questions/48675520/hardcoding-or-substituting-char-argv-in-c" %}

![](<../.gitbook/assets/image (236) (1).png>)

![](<../.gitbook/assets/image (20) (1).png>)

![first(argv\[0\]) argument is the program itself's name. Generally ignored. and last argument must be followed by NULL for system to be notifed as the termination. Then argv\[\] is initialized as const.](<../.gitbook/assets/image (219) (1).png>)
