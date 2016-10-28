---
layout: post
title: "Sieć WiFi nie działa po wyjściu laptopa z uśpienia"
date: 2014-04-12 08:35:16 +0200
comments: true
categories: 
---
Przy próbie naprawy połączenia można doszukać się komunikatu: "System Windows nie mógł automatycznie powiązać stosu protokołu IP z kartą sieciową".
Dobrze spróbować zresetować protokół TCP/IP jako administrator:

``` bat
netsh int ip reset
```

Działa w Windows Vista, 7, 8 i 8.1.

[Źródło](http://support.microsoft.com/kb/299357/pl)