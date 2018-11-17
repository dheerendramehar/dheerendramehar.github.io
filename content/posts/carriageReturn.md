+++
title = "Carrige return(\\r) addition to a file in Windows"
date = 2018-09-23T10:26:48+05:30
tags = [""]
categories = [""]
draft = false
+++



## 1. Problem

While writing a bash script in Unix, i found that if i create a file in Windows and use it it in a bash script, script fails. When digging deeper into the issue, i got to know that this was due to carriage return(\r), which was added when i modified the file in Windows(\r).



## 2. Basics

In old days when people had to use Typewriters, they had to do two things frequently

<img src="/posts/images/typewriter.jpg" alt="drawing" width="200"/>

>a. Move carriage to the beginning of the line to
restart typing (\r)

>b. Turn wheel to move the paper to change the line (\n)



A carriage return(\r) means moving the cursor to the beginning of the line.

A line feed(\n) means moving one line forward. Windows often still uses Typewriter's scheme i.e. combination of both as \r\n in text files.

Unix mostly uses only the \n.

## 3. Solution

First check whether file contains a “\r” at the end (0d in Hex) or not using the following command.

```bash
$ while read -r line; do printf  %s "$line" | xxd; done < file.txt
```
 >xxd: creates a hex dump of a given file or standard input

If the $line contains a \r (CR) at the end (0d). Remove it with ${line%$'\r'}. You can use either of the following commands
```bash
$ while read -r line; do echo ${line%$'\r'} >> tmp.txt ; done < file.txt
```
or
```bash
$ tr -d '\r' < file.txt > tmp.txt
$ while read -r line; do printf  %s "$line" | xxd; done < tmp.txt
```

If you run the above commands then your file(tmp.txt) will be carriage return(\r) free and you can use it in Unix/Linux Systems without any issues.

## 4. Example

a. Create a file in Unix and check it's Hex Dump

```bash
[admin@localhost ~]$ vi file.txt
[admin@localhost ~]$ cat file.txt
love
hate
[admin@localhost ~]$ while read -r line; do printf  %s "$line" | xxd; done < file.txt
0000000: 6c6f 7665                                love
0000000: 6861 7465                                hate
```
 b. Now create another file named 'file2.txt'  with same content in windows and import it into Unix.
```bash
[admin@localhost ~]$ while read -r line; do printf  %s "$line" | xxd; done < file2.txt
0000000: 6c6f 7665 0d                             love.
0000000: 6861 7465 0d                             hate.
[admin@localhost ~]$ cat file2.txt
love
hate
```

c. Can you see the extra addition of "0d" in Hex Value or '.' in word name? while cat shows the same output in both operating systems. That extra '0d' is due to addition of carriage return(\r) at the end of every line in windows.

So let's remove this;
```bash
[admin@localhost ~]$ tr -d '\r' < file2.txt > tmp.txt
```
or
```bash
[admin@localhost ~]$ while read -r line; do echo ${line%$'\r'} >> tmp.txt ; done < file.txt
[admin@localhost ~]$ while read -r line; do printf  %s "$line" | xxd; done < tmp.txt
0000000: 6c6f 7665                                love
0000000: 6861 7465                                hate
[admin@localhost ~]$ cat tmp.txt
love
hate
```

So we have removed that extra "0d" and now we are good to use this file in Unix/Linux. Note that "cat" still shows the same output because it does not print escape characters.



## 5. More info

>Parameter expansion : ${var%Pattern} removes from $var the shortest part of $Pattern that matches the back end of $var.

>Why is the $ needed before the '\r'?
Ans: There are two characters in '\r', backslash and r; while $'\r' is one character, the carriage return. We use $'...' when we want to escape sequences to be interpreted by the shell. To know more read ‘Ansi-C Quoting’.

