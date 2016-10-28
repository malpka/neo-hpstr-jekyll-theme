---
layout: post
title: "Migrate mail account to outlook.com with offlineimap"
date: 2016-02-22 19:07:00 +0200
comments: true
categories: bash, linux
---

You can try an `offlineimaprc` file like below:

```
[general]
accounts = Email-Sync

[Account Email-Sync]
remoterepository = old_server
localrepository = new_server

[Repository old_server]
type = IMAP
remotehost = poczta.o2.pl 
remoteuser = u_s_e_r
maxconnections = 1
readonly = true
folderfilter = lambda folder: folder not in ['Trash']

[Repository new_server]
type = IMAP
remotehost = imap-mail.outlook.com
remoteuser = user@outlook.com
ssl = yes
maxconnections = 1
cert_fingerprint = c914dd966dbd0912c36ec294f83d8d3b5a434729
createfolders = false
```

If you get a message with invalid ssl cert, just update/insert the line with a proper value of cert_fingerprint. 
It shoud be next to the error message
