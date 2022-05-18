# emb29: Let's write binary myself(terrifying)

{% embed url="https://linuxhint.com/c_programming_examples_linux_beginners" %}

{% embed url="https://linuxconfig.org/c-programming-tutorial" %}

fork() creates the child process while exec\*() replaces current process

### Helpful stuff <a href="#helpful-stuff" id="helpful-stuff"></a>

* For launching programs from Python, we recommend using [pwntools](https://docs.pwntools.com/en/stable/intro.html), but [subprocess](https://docs.python.org/3/library/subprocess.html) should work as well. If you are not using one of these two, you will suffer heavily when you get to input redirection (for that, check out the `stdin` and `stdout` arguments to `pwn.process` or `subprocess.Popen`).
* For reading and writing directly to file descriptors in bash, check out the `read` and `echo` builtins.
* You will find the `env` command useful, and the `exec` bash builtin.
* Quick refreshers on `fork()` versus `exec*()` [here](https://www.geeksforgeeks.org/difference-fork-exec/) and [here](https://linuxhint.com/linux-exec-system-call/) and [here](https://iximiuz.com/en/posts/how-to-on-processes/).
* Remember to `wait()` on your children! If you use `subprocess.Popen`, `pwn.process`, or good old `fork()`, your parent will keep executing and, unless it waits for the child in some way, will just terminate! This is almost never what you want.
* Some [documentation](https://www.binarytides.com/socket-programming-c-linux-tutorial/) on networking in C.
* Useful resource for [pipes in C](https://jameshfisher.com/2017/02/17/how-do-i-call-a-program-in-c-with-pipes/).
* Useful resource for [FIFOs in C](https://www.geeksforgeeks.org/named-pipe-fifo-example-c-program/).
* A treatise on I/O redirection in Linux shells, which has applications in this assignment: [https://bencane.com/2012/04/16/unix-shell-the-art-of-io-redirection/](https://bencane.com/2012/04/16/unix-shell-the-art-of-io-redirection/)
* A guide on Linux symbolic links. [https://www.nixtutor.com/freebsd/understanding-symbolic-links/](https://www.nixtutor.com/freebsd/understanding-symbolic-links/)
* A video tutorial on [FIFOs in C](https://www.youtube.com/watch?v=2hba3etpoJg).
* A great [visual guide to I/O redirection in Linux](http://www.rozmichelle.com/pipes-forks-dups/).
* An incredible [pwntools cheatsheet](https://gist.github.com/anvbis/64907e4f90974c4bdd930baeb705dedf) by a pwn.college student!

This chapter for fork() and exec\*()

### level29\~35：c语言 <a href="#h2-7" id="h2-7"></a>

这个给了很多提示，大概是因为这个更涉及原理吧，原文如下：

```
[INFO] This challenge will now perform a bunch of checks.[INFO] If you pass these checks, you will receive the flag.[TEST] Performing checks on the parent process of this process.[TEST] Checking to make sure that the process is a custom binary that you created by compiling a C program[TEST] that you wrote. Make sure your C program has a function called 'pwncollege' in it --- otherwise,[TEST] it won't pass the checks.[HINT] If this is a check for the *parent* process, keep in mind that the exec() family of system calls[HINT] does NOT result in a parent-child relationship. The exec()ed process simply replaces the exec()ing[HINT] process. Parent-child relationships are created when a process fork()s off a child-copy of itself,[HINT] and the child-copy can then execve() a process that will be the new child. If we're checking for a[HINT] parent process, that's how you make that relationship.[INFO] The executable that we are checking is: /usr/bin/bash.[HINT] One frequent cause of the executable unexpectedly being a shell or docker-init is that your[HINT] parent process terminated before this check was run. This happens when your parent process launches[HINT] the child but does not wait on it! Look into the waitpid() system call to wait on the child!​[HINT] Another frequent cause is the use of system() or popen() to execute the challenge. Both will actually[HINT] execute a shell that will then execute the challenge, so the parent of the challenge will be that[HINT] shell, rather than your program. You must use fork() and one of the exec family of functions (execve(),[HINT] execl(), etc).[FAIL] You did not satisfy all the execution requirements.[FAIL] Specifically, you must fix the following issue:[FAIL]    The process must be your own program in your own home directory.
```

总之，总结一下看出来的知识点：

1. 对父进程的检测需要使用exec()系列的函数，因为system()或popen()函数都会执行一个shell，然后用shell来执行，所以此时父进程为shell（测试后是dash），而不是你的程序。
2. 而exec()只是替换掉正在exec()的进程，当用fork()函数时子进程调用exec()系列函数杀死自己的子进程副本的时候就会建立与当前主进程的父子关系。
3. 当一个父亲创建了一个孩子但没有等它结束就自己结束的话就可能造成系统异常，查询waitpid()的使用来等待孩子进程。

另外查询了一下，说是exec系统调用，实际上在Linux中，并不存在一个exec()的函数形式，exec指的是一组函数，一共有6个，分别是：(meaning, linux has family of 6 exec functions)

```
#include <unistd.h>int execl(const char *path, const char *arg, ...);int execlp(const char *file, const char *arg, ...);int execle(const char *path, const char *arg, ..., char *const envp[]);int execv(const char *path, char *const argv[]);int execvp(const char *file, char *const argv[]);int execve(const char *path, char *const argv[], char *const envp[]);
```

然后整理了一下基本使用：

```
#include <stdio.h>#include <unistd.h>​void pwncollege(char* argv[],char *env[]){    execve("/challenge/embryoio_level29",argv,env);//使用exec系列函数执行时不会改变新进程的父亲，相当于只是将当前进>程替换掉了    return ;}​int main(int argc,char* argv[],char* env[]){    pid_t fpid;​    fpid=fork();//fork()执行之后，会复制一个基本一样的进程作为子进程，然后两个进程会分别执行后面的代码    if(fpid<0)//如果fpid为-1，说明fork失败            printf("error in fork!\n");    else if (fpid==0){//成功则会出现两个进程，fpid==0的是子进程            printf("我是子进程\n");            pwncollege(argv,env);    }    else{//fpid==1的是父进程            printf("我是父进程\n");            wait(NULL);    }    return 0;}
```

\#include \<stdio.h>

\#include \<unistd.h>

![](<../.gitbook/assets/image (128).png>)

然后又是一次轮回。

注意，设定参数数组时，第一个不是参数而是文件名，而且最后需要加NULL（因为数组最后一位需要为\0吧。），这两个任意错了一步就会导致运行子进程失败：

```
#include <stdio.h>#include <unistd.h>​void pwncollege(char* argv[],char *env[]){    char *newargv[]={"embryoio_level31","scfxabffgf",NULL};    execve("/challenge/embryoio_level31",newargv,env);//使用exec系列函数执行时不会改变新进程的父亲，相当于只是将当前>进程替换掉了    return ;}​int main(int argc,char* argv[],char* env[]){    pid_t fpid;​    fpid=fork();//fork()执行之后，会复制一个基本一样的进程作为子进程，然后两个进程会分别执行后面的代码    if(fpid<0)//如果fpid为-1，说明fork失败            printf("error in fork!\n");    else if (fpid==0){//成功则会出现两个进程，fpid==0的是子进程            printf("我是子进程\n");            pwncollege(argv,env);    }    else{//fpid==1的是父进程            printf("我是父进程\n");            wait(NULL);    }    return 0;}
```

![](<../.gitbook/assets/image (192).png>)

