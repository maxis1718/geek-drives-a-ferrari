SSHFS
---


###Requirement: `sshfs`

Download packages [Here](http://osxfuse.github.io/). (for Mac)


###Mount a remote folder


mkdir `<local-mount-point>`

sshfs `<hostname>`:`<remote-path>` `<local-mount-point>`


e.g.,

```
mkdir doraemon-corpus
sshfs -P 2222 <your-username>@doraemon.iis.sinica.edu.tw:/corpus doraemon-corpus
```

Now we can use GUI or IDE to write codes and execute the program just like local files ☺︎

![img](img/sshfs.png)
