# emb5: redirection

{% embed url="https://www.bing.com/search?FORM=ANNTA1&PC=U531&aqs=edge..69i57.9639j0j1&cvid=f146a83d38ae4e0db39245d588fc7b04&pglt=2083&q=how+to+redirect+stdin+in+linux" %}

{% embed url="https://stackoverflow.com/questions/26132393/redirecting-stdin-c?msclkid=e48b1a5acffe11ecba2866146a47379b" %}

#### [https://www.guru99.com/linux-redirection.html?msclkid=5f80a000d00011ec8f45e9738a3f6040](https://www.guru99.com/linux-redirection.html?msclkid=5f80a000d00011ec8f45e9738a3f6040)



#### Simultaneous Redirection

In the example above, the **stderr** stream was identified by its numeric identifier – this means you can redirect **stdout** and **stderr** in the same command by specifying which one you wish to redirect:

echo "hello there! 1>test.txt 2>error.txt

Above, **stdout** is sent to _test.txt,_ and **stderr** is sent to _error.txt_.

#### Piping

Piping is the same as redirection, but it only deals with **stdin**, and **stdout** errors are ignored.

echo "hello there!" | cat

Here, the pipe (**|**) pipes (redirects) **stdout** of the _echo_ command to **stdin** of the _cat_ command.



#### Redirection

Usually, the _echo_ command will print text to the console:

echo "hello there!"

The **stdout** of the echo program is taking its default path to be displayed on your screen.

_Redirection_ lets you send it somewhere else. Here, it is sent to a file:

echo "hello there!" > test.txtA file called _text.txt_ will be created containing the text _“hello there!”_ (**watch out, if the file already exists, it will be overwritten**).

_You can append files by using **>>** instead of **>**_

Next, let’s redirect **stdin** using **<**

cat < test.txt

[The _cat_ command](https://www.linuxscrew.com/?p=7172) reads the contents of **text.txt** into its **stdin** stream and then does what the _cat_ command is designed to do – prints the data supplied to it to **stdout**, which by default is the console for viewing. So, this will simply output _hello there!_ to the console.

