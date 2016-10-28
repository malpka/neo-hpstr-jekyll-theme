---
layout: post
title: "Wyrażenia regularne w praktyce - wyszukiwanie i zamiana"
date: 2014-01-04 15:51
comments: true
published: false
---

RegEx są na prawdę przydatne do przetważania wszelkiego rodzaju danych tekstowych.

Potrzebne mi były dane z [cennika domen OVH](http://www.ovh.pl/domeny/cennik_domen.xml), 
ale w formie możliwej do przekazania do arkusza kalkulacyjnego. Bezpośrednie wklejenie 
tabeli do LibreOffice nie wygląda najlepiej:

{% img https://lh6.googleusercontent.com/-0bI9_6gW98g/Sdj0w1QGWcI/AAAAAAAABt4/gdLqSJf4ZTs/s144/IMG_1940.JPG 600 300 Cennik OVH xls %}
{% img http://placekitten.com/890/280 %}


Zlikwiduję całkowicie znaki końca linii:
```
^(\.[a-zA-Z \*\.]+)\t\( ([0-9,]+).*\( ([0-9,]+).*
```