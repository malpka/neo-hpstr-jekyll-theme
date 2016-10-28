---
layout: post
title: "Tunelowanie Zdalnego Pulpitu w celu ominięcia NAT"
date: 2007-03-03 22:59
comments: true
categories:
- Linux
- Ogólne
---

``` bash
$ ssh -R 50000:localhost:3389 flytothesky@quiz.game-host.org
$ rdesktop quiz.game-host.org -p 50000
```

warunek: (`GatewayPorts yes` w `/etc/ssh/sshd_config`).

Jeżeli jest wyłączone, to można jeszcze spróbować dodatkowo:

z domu:

``` bash
$ ssh -L 3389:localhost:50000 flytothesky@quiz.game-host.org
$ rdesktop localhost
```
		