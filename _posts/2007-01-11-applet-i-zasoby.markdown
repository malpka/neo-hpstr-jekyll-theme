---
layout: post
title: "Applet i zasoby"
date: 2007-01-11 07:23
comments: true
categories:
- Programowanie
---
<p>Jeden ze znajomych miał problem z dołączeniem plików grafiki do appletu.<br>
Jak wiadomo polityka zabezpieczeń appletów jest słusznie bardzo ograniczona:</p>
<ul>
<li>brak możliwości korzystania z lokalnego systemu plików</li>
<li>możliwość podłączenia jedynie z serwerem z appletem</li>
</ul>
<p>Okazuje się, że aby korzystać w applecie z zewnętrznych danych wystarczy skorzystać z <i>zasobów</i>. Pozwalają na odwoływanie się do systemu plików względem ścieżki w której znajduje się wykonywany plik .class:</p>
<p></p>
``` java
InputStream in = getClass().getResourceAsStream("obrazy/czolg1.png");
```