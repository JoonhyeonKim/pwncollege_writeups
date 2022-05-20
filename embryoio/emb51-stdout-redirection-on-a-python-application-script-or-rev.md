# emb51:stdout redirection on a python application, script | rev

To achive rev | rev |, one should send EOF in script

{% embed url="https://stackoverflow.com/questions/66011026/how-to-send-an-eof-to-a-process-server-in-pwntools" %}
&#x20;you can send it an EOF mark with `p.send(b'\4')`
{% endembed %}

![](<../.gitbook/assets/image (23) (1).png>)

But seems bit convoluted.

![](<../.gitbook/assets/image (45).png>)

So do the easier way

![](<../.gitbook/assets/image (142).png>)
