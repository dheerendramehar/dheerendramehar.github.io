+++
title = "How to get Internet on a server using Squid Proxy and SSH port forwarding"
date = 2018-12-27T00:39:22+05:30
tags = [""]
categories = [""]
draft = false
+++


Do the setup as follows:

**Setup on Host A:**

1. Install proxy server Squid on Host A . By default Squid listens on port 3128.  
```yum install squid```
2. Comment the ```http_access deny all``` then add ``http_access allow all`` in /etc/squid/squid.conf
3. If Host A itself uses some proxy say 10.140.78.130:8080 to connect to internet then also add that proxy to ```/etc/squid/squid.conf``` as follows:
  ```
refresh_pattern (Release|Packages(.gz)*)$ 0 20% 2880
cache_peer 10.140.78.130 parent 8080 0 no-query default
never_direct allow all
```

**Setup on Host B:**

1. Add the following entries to /etc/environment
```
export http_proxy=http://127.0.0.1:3129
export https_proxy=http://127.0.0.1:3129
```
2. ```source /etc/environment```

Now our setup is complete.

**Creating SSH tunnel with Remote port forwarding**

1. Run the follwoing SSH command from Host A  
```ssh -R 3129:localhost:3128 user@HostB```
2. This will allow Host B to access the internet through Host A.

**Checking the internet:**

1. Run the following command from Host B  
```wget https://google.com```

**Traffic flow diagram** :
[![enter image description here][1]][1]


  [1]: https://i.stack.imgur.com/NSVV7.jpg
