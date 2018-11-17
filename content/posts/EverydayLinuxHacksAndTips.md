+++
title = "Everyday Linux hacks and tips"
date = 2018-10-07T11:08:35+05:30
tags = [""]
categories = [""]
draft = false
+++

*Here are some useful linux commands, i frequently use*

## 1. Removing *grep* result from ps output
>### ps aux | grep [d]hcp

By putting brackets, we are searching for a regex and preventing grep from matching itself. Since [d]hcp doesn't match the [d]hcp regular expression, 
so grep won't show up in the results.  
To understand more, play with *ps*, *grep* and *regex*.  
Below is the ouput of above command with and without brackets.
```bash
[root@localhost ~]# ps aux | grep dhcp
   53 root     dhcpcd
   97 root     grep dhcp
[root@localhost ~]# ps aux | grep [d]hcp
   53 root     dhcpcd
```

For more information, have a look at this StackExchange's [answer](https://unix.stackexchange.com/a/74186).



