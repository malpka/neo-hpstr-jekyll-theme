---
layout: post
title: "Own mailserver - Debian 7 Wheezy VPS - Part 1 - basic mailserver"
date: 2014-07-15 07:47:59 +0200
comments: true
categories: vps, linux
---

## Check / set up machine's hostname

``` bash
malpka@codemonkey:~$ hostname
codemonkey.pl
```

## Set up DNS record

```
@  IN MX  1	codemonkey.pl 
@  IN TXT "v=spf1 a mx ~all"
```

## Check SMTP (25) port for outside availability

## Install postfix

```
apt-get install postfix
```

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/postfix-install-1.png %}

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/postfix-install-2.png %}

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/postfix-install-3.png %}

## Voila! ;)

Check if we have access to `mail` command

```
apt-get install mailutils
```

and send the mail (end with Ctrl+D)

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/postfix-install-4.png %}

Mail received, post reply

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/first-mail-received.png %}

After posting the reply

{ % img https://dl.dropboxusercontent.com/u/119311219/blog.codemonkey.pl/images/mailserver/first-reply-received.png %}

## Configure mail aliases

## In `/etc/aliases` file we can add redirections between local users

``` bash
codemonkey:~# tail -n 1 /etc/aliases
root: malpka
codemonkey:~# newaliases
```

## Remarks

- be aware of STMP relay security! [SMTPD_ACCESS_README.html](http://www.postfix.org/SMTPD_ACCESS_README.html)
- works for any local system user
- uses `/var/mail/{username}` as a default mailbox location and `MBox` as a format
- mail servers like gmail will reject e-mails from our mailserver until the RevDNS and SPF record are properly configured.

