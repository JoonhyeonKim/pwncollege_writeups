---
description: >-
  in short, fork() creates new child process(pid=0) thus changing pid while
  exec*() replaces current process thus maintaing current pid.
---

# 🟢 fork() and exec\*()\*

meaning, you must start with fork(). since exec\*() doesn't create new pid.(That's why when pid=0, you can perform exec\*(), pid=0 => I am a child. if pid>0, I am a parent.). fork()like create, exec\*()ex

{% embed url="https://iximiuz.com/en/posts/how-to-on-processes" %}

![pid\_t data type](<../.gitbook/assets/image (60) (1) (1).png>)

![fork() creates a new process by duplicating the calling process](<../.gitbook/assets/image (111) (1).png>)

![The exec() family of functions replaces the current process image with a new process image](<../.gitbook/assets/image (43).png>)

![](<../.gitbook/assets/image (47) (1).png>)

![](<../.gitbook/assets/image (181) (1).png>)

![](<../.gitbook/assets/image (48).png>)

![](<../.gitbook/assets/image (131).png>)

![](<../.gitbook/assets/image (112) (1).png>)

![](<../.gitbook/assets/image (59) (1) (1) (1) (1).png>)

![](<../.gitbook/assets/image (18) (1) (1) (1) (1) (1).png>)

![](<../.gitbook/assets/image (161).png>)

![v for argv\[\] as vector](<../.gitbook/assets/image (99) (1) (1).png>)

![](<../.gitbook/assets/image (30) (1).png>)

![](<../.gitbook/assets/image (26) (1).png>)

![Observe the exactly same PID](<../.gitbook/assets/image (35) (1) (1).png>)

![](<../.gitbook/assets/image (150).png>)
