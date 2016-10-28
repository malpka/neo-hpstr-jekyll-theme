---
layout: post
title: "HOWTO test local network speed"
date: 2014-07-15 07:47:59 +0200
comments: true
categories: networking linux
---
I have a problem to determine where is my LAN's bottleneck. Copying files between two computers should be faster. Let's check it out.

To mesure the speed we will prepare a client-server connectionL

1. Preparation

Install netcat on machines that will take part in the tests.
On a OpenWRT router we can install it through a package manager.

`opkg update`
`opkg install bash netcat`

2. Server

`nc -l -p 1122 > /dev/null`

3. Client

`dd if=/dev/zero bs=10000 count=1 | nc 192.168.1.3 1122`

4. Results

```
malpka@micromalpki:~$ dd if=/dev/zero bs=100M count=1 | nc 192.168.1.3 1122
1+0 przeczytanych recordów
1+0 zapisanych recordów
skopiowane 104857600 bajtów (105 MB), 13,6733 s, 7,7 MB/s
```

