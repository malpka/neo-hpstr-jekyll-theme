---
layout: post
title: "Przekierowanie portu Windows"
date: 2014-04-30 11:28:25 +0200
comments: true
categories: 
facebook:
    image: http://i.imgur.com/mNHnpU9.png
---

{% img left http://i.imgur.com/mNHnpU9.png 96 96 cmd %}

Przekierowanie lokalnego portu na systemie z Windowsem na zdalny na zewnętrznej maszynie.

&nbsp;

``` bat
netsh interface portproxy add v4tov4 listenport=3390 listenaddress=192.168.1.20 connectport=3389 connectaddress=81.81.81.81
```

- listenport - port nasłuchujący lokalnie
- listenadress - adres na lokalnej maszynie, na którym nasłuchiwać, można hurtowo 0.0.0.0
- connectport - port docelowy
- connectaddress - adres komputera docelowego

Aby skasować jedno przekierowanie:

``` bat
netsh interface portproxy delete v4tov4 listenport=3390 listenaddress=192.168.1.20
```

Aby skasować wszystkie:

``` bat
netsh interface portproxy reset
```

Aby zobaczyć stan:
``` bat
netsh interface portproxy show all
```

