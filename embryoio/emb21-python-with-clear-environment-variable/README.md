# emb21: python with clear environment variable

![](<../../.gitbook/assets/image (185) (1) (1).png>)

![](<../../.gitbook/assets/image (115).png>)



Quite a few. `env` runs a command with a modified environment. For example, `env -i` will run it with an empty environment.

```
$ env -i ./countenv
There are 0 environment variables.
```

I can also use `env` to set environment variables.

```
$ env -i NAME=Yan JOB=Professor ./countenv
There are 2 environment variables.
```

then env -i python also possible?

I am not sure

![](<../../.gitbook/assets/image (179) (1) (1).png>)
