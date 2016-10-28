---
layout: post
title: "Migracja Jogger - Octopress"
date: 2014-01-05 17:06
comments: true
categories: 
---

## tl;dr ##

<a href="#skrypt">Skrypt</a> w pythonie 3 przetwarzający plik xml z danymi Joggera na pliki .markdown gotowe do wrzucenia do `source/_posts/` w Octopressie


## Pobieranie danych z Joggera ##

Dane z Joggera można pobrać z panelu administracyjnego: ```Opcje → Eksport → Wygeneruj eksport → Pobierz```
Są one w formacie XML, spakowane gz. Odpowiednio sformatowane prezentują się jak poniżej:

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<jogger>
  <user>
    <jid>malpka@przykladowy.jid</jid>
    <domain>malpka</domain>
    <alias/>
  </user>
  <entry>
    <date>2007-01-11 00:29:07</date>
    <jid>malpka@przykladowy.jid</jid>
    <level_id>1</level_id>
    <comment_mode>0</comment_mode>
    <subject>temat</subject>
    <body>
      &lt;p&gt;tresc tresc tresc&lt;/p&gt;
    </body>
    <tags/>
    <permalink>temat</permalink>
    <trackback/>
    <category>Ogólne</category>
    <category>Inna kategoria</category>
    <comment>
      <date>2007-01-11 03:35:52</date>
      <nick>NickKomentujacy</nick>
      <nick_url>http://google.pl</nick_url>
      <body>&lt;p&gt;*wpadłem bo spać nie mogę :)*&lt;/p&gt;</body>
      <ip>127.0.0.1</ip>
      <trackback/>
    </comment>
  </entry>
    ...
</jogger>
```
Oczywiście wartość gałęzi `body` to escapowany html wpisu.

W razie czego można wygenerować sobie [XSD z XML](/2014/01/06/tworzenie-schematu-xsd-z-xml/).

## Przetwarzanie danych eksportu na wpisy Octopressa ##

Skoro już wiadomo co i jak, można pokusić się o wyciągnięcie podstawowych informacji z XML'a: daty, tytułu, permalinka (który potraktuję jako część nazwy pliku), kategorii i treści wpisu.
Przy okazji wyszło, że Jogger pozwalał na ustawienie pustego tytułu wpisu, co skutkuje brakiem wartości taga ```<subject/>```

Tym razem python 3.

<a name="skrypt"></a>
Sposób użycia:

* rozpakować plik z danymi eksportu jako ```jogger_eksport.xml```, najlepiej do osobnego katalogu
* umieścić skrypt razem z plikiem xml
* uruchomić skrypt
* w katalogu dla każdego wpisu powstanie osobny plik ```.markdown```, nazwany zgodnie z regułami Octopressa, z uzupełnionymi polami: tytuł, data, kategorie, oraz z treścią posta wpisaną w HTML'u

{% gist 8273337 %}

TODO:

* zachowanie treści szkiców (to już trzeba ręcznie)
* zmiana treści na markdown