---
layout: post
title: "Own mailserver - Debian 7 Wheezy VPS - Part 2 - virtual domains"
date: 2014-07-15 07:47:59 +0200
comments: true
categories: vps, linux
---

## Add a domain to postfix configuration - temporary solution [src](http://www.postfix.org/VIRTUAL_README.html#local)

``` bash
postfix -e mydestination="example.org, example.com, example.net"
```

Now local users receive mails from all domans, i.e. user `malpka` will receive mails from `malpka@example.org`, `malpka@example.com` and `malpka@example.net`.
Mails are saved in `/var/mail/malpka`

## Separate mail from UNIX-accounts

### Add vmail directory and vmail user

``` bash
mkdir -p /var/vmail
groupadd -g 5000 vmail
useradd -g vmail -u 5000 vmail -d /var/vmail -m
chown -R vmail:vmail /var/vmail
chmod u+w /var/vmail
```

### Reconfigure postfix to use virtual

Let's add a mail subdomain

```
example.org   IN MX	1	example.com 
```

Postfix reconfiguration

``` bash
postconf -e virtual_mailbox_domains=example.org
postconf -e virtual_mailbox_base=/var/vmail
postconf -e virtual_mailbox_maps=hash:/etc/postfix/virtual_mailbox_maps
postconf -e virtual_minimum_uid=100
postconf -e virtual_uid_maps=static:5000
postconf -e virtual_gid_maps=static:5000
postconf -e virtual_alias_maps=hash:/etc/postfix/virtual_alias_maps
```

- `virtual_mailbox_domains` - comma separated list of domains that are handled by postfix' virtual domains mechanism. The rest (from `mydestination`) is handled as a local mail.
- `virtual_mailbox_base` - base folder for virtual mailboxes. This is the prefix that is prepended to the items from `virtual_mailbox_maps`
- `virtual_mailbox_maps` - location of mailboxes for accounts
- `virtual_minimum_uid` - safety reasons
- `virtual_uid_maps`, `virtual_gid_maps` - user/group for writing 

Domain listed in `virtual_mailbox_domains` must not be present in `mydestination`

Mailbox maps

``` bash
echo "malpka@example.org example.org/malpka" >> virtual_mailbox_maps
echo "@example.org example.org/catchall" >> virtual_mailbox_maps
```

If you would like to use Maildir format instead of MBox, just add slash (example.org/malpka/)

Aliases

```
echo "malpka2@example.org malpka" >> virtual_alias_maps
```

Hash configuration files

``` bash
postmap virtual_alias_maps
postmap virtual_mailbox_maps
```

Create mailbox file and setup permission again.

``` bash
touch /var/vmail/example.org/malpka
touch /var/vmail/example.org/catchall

chown -R vmail:vmail /var/vmail
chmod u+w /var/vmail
```

Reload postfix configuration

``` bash
postfix reload
```

### Test

Receive mail.

``` bash
mutt -f /var/vmail/example.org/malpka
```

### Remarks

- Despite every email address has it's own place (different MBox/Maildir) you can only access it from the local system (root or vmail user). Fix in Part 4 - dovecot.
- the mails that you send from a local accounts will still be from `$myorigin` domain
- [MBox vs Maildir war](http://www.linuxmail.info/mbox-maildir-mail-storage-formats/)
- postfix virtual_* configuration can be moved to a database, when needed (more users)
