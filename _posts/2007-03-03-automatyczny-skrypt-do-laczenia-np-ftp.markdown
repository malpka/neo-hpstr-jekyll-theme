---
layout: post
title: "Automatyczny skrypt do łączenia (np FTP)"
date: 2007-03-03 22:33
comments: true
categories:
- Linux
---
<p>Za pomocą poniższego skryptu możemy zautomatyzować połączenie z serwerem (przy założeniu że mamy zainstalowany pakiet expect)<br>
jeśli nie to (Ubuntu) `sudo apt-get install expect`</p>

``` bash
#!/usr/bin/env expect

set username yourUsername
set pass yourPasswd
set host theHost

spawn ftp ${username}@${host}
expect "Password:"
send "${pass}\r"
expect "ftp&gt; "
interact
````

Szczerze mówiąc potrzebna mi była wersja przerobiona na ssh, w połączeniu z powyższym postem. Jeszcze tylko wrzucenie do autostartu i będzie linuxowy "trojan" ;) dla osoby znajdującej się za natem</p>
		