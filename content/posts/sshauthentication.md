+++
title = "Resolving SSH Authentication issues"
date = 2018-09-28T22:14:40+05:30
tags = ["ssh","SSH Authentication", "SSH Keys", "Linux"]
categories = ["LinuxTips"]
draft = false
+++

# How to resolve SSH Authentication issues

## 1. Problem:
I wanted to access an Ubuntu node from a CentOS node without any password. To accomplish this, i needed to setup SSH keys. So I followed the following steps:

a. Generated SSH keys using ssh-keyzen
```bash
ubuntu@ubuntu_node:~$ ssh-keygen
```
here two keys are generated */your_home/.ssh/id_rsa* and */your_home/.ssh/id_rsa.pub* . First one is private key and second is public key.

b. Copy the public key to authorized_keys on remote node(in my case a CentOS node) using ssh-copy-id
```bash
ubuntu@ubuntu_node:~$ ssh-copy-id centos@ubuntu_node_IP
```

c. Check on remote node whether the Public key is added in authorized_keys.
```bash
ubuntu@ubuntu_node:~$ less ~/.ssh/authorized_keys
```

Above three steps worked without any error but still i wasn't able to do SSH to my CentOS node. So after playing with the system and doing some research on internet, i have made my **Golden Procedure** to debug such issuee without wasting time.

## 2. Golden Procedure:
### 1. To be able to do SSH from one node to another, ensure that SSHD dameon is running on both nodes.
```bash
ubuntu@ubuntu_node:~$ ps aux | grep [s]shd
root       298  0.0  2.1  65308  5124 ?        Ss   15:54   0:00 /usr/sbin/sshd -D 
```
```
centos@centos_node:~$ ps aux | grep [s]shd
root       298  0.0  2.1  65508  5424 ?        Ss   15:55   0:00 /usr/sbin/sshd -D    
```                                              
### 2. Now run the SSH in debug mode. This can be done by using -v option in ssh command

```bash
ubuntu@ubuntu_node:~$ ssh -v  -i ~/.ssh/id_rsa centos@10.140.100.66
OpenSSH_7.2p2 Ubuntu-4ubuntu2.2, OpenSSL 1.0.2g  1 Mar 2016
debug1: Reading configuration data /home/ubuntu/.ssh/config
debug1: Connecting to 10.140.100.66 [10.140.100.66] port 22.
debug1: Connection established.
debug1: identity file /home/ubuntu/.ssh/id_rsa 
debug1: Authenticating to 10.140.100.66:22 as 'centos'
debug1: SSH2_MSG_KEXINIT sent
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Next authentication method: gssapi-keyex
debug1: No valid Key exchange context
debug1: Next authentication method: gssapi-with-mic
debug1: Unspecified GSS failure.  Minor code may provide more information
debug1: Next authentication method: password
centos@10.140.100.66's password:
```
Pay attention to any error that comes in ssh ouput. 
Here in my case, despite passing private key, it is falling to password based authetication.

### 3. Check the remote node's authentication logs

> For CentOS: check logs in /var/log/secure file  
> For Ubuntu: Check logs in /var/log/auth.log

My remote node is CentOS. Logs in *secure* file are:
```bash
centos@centos_node:~$ tail -f /var/log/secure
Sep 28 15:41:40 nvmbd2akl150d00 sshd[15433]: Authentication refused: bad ownership or modes for directory /home/centos
```

Here it is showing "bad ownership or modes for directory /home/centos". So i correted the permissions.  
Generally, you will be able to find any issues in these logs. 
>And to fix that *do what logs says*.

 In my case centos node was not having correct home directory permissions. After correcting the permissions to 700, authetication issue was resolved.
 ```bash
centos@centos_node:~$ chmod 700 /home/centos
```
 
 After corecting the permissions, /var/log/secure output is as follows:
```bash
centos@centos_node:~$ tail -f /var/log/secure
Sep 28 15:54:07 nvmbd2akl150d00 sshd[44948]: Accepted publickey for userapp from 10.147.106.37 port 40836 ssh2
```

 I hope, above steps will help you to debug your SSH issues.


