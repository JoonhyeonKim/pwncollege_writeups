# emb118: stdin from fifo1 and bin's stdout to fifo2 and fifo2's stdin

![FIFOs are funny things. If a process tries to open one for reading, it will block until there's a process that opens it for writing. Conversely, if a process tries to open one for writingt, it will block until there's a process that opens it for reading. However, multiple processes can open it for reading or writing](<../.gitbook/assets/image (2).png>)

![Then from the other terminal< send a string to first fifo.](<../.gitbook/assets/image (95).png>)
