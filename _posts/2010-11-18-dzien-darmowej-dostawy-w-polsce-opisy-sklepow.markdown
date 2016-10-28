---
layout: post
title: "Dzień Darmowej Dostawy w Polsce - opisy sklepów."
date: 2010-11-18 10:09
comments: true
categories:
- Programowanie
- Python
---
<p>Ostatnio dowiedziałem się o akcji <b>Dzień Darmowej Dostawy</b>, która odbędzie się 1 grudnia 2010 r., wzorowanej na amerykańskim Free Shipping Day. Cel jest oczywisty, a szczegółowe informacje są podane na stronie <a href="http://dziendarmowejdostawy.pl/">http://dziendarmowejdostawy.pl/</a>.</p>
<p>Firmy uczestniczące w akcji są wymienione w formie adresów internetowych stron, bez odsyłaczy. Poza bardziej znanymi partnerami akcji jak gram.pl, Vobis, Helion, Komputronik czy Megastore jest sporo sklepów, o których działalności niewiele można powiedzieć po samym adresie internetowym. Parę przykładów - Fnak.pl, DeeZee.pl, Maminek.pl, KissMyKicks.pl czy KolorowaKrowa.pl ! :)</p>
<p>W celu szybkiego sprawdzenia tematyki każdego ze sklepów popełniłem mały skypcik w <b>pythonie</b>, w którym widać łatwość z jaką można wkroczyć w tematykę zwaną <a href="http://en.wikipedia.org/wiki/Web_scraping">Web scraping</a></p>

``` python
import urllib, sys, BeautifulSoup

adresDDD = "http://dziendarmowejdostawy.pl/"
soup = BeautifulSoup.BeautifulSoup(urllib.urlopen(adresDDD))

for li in soup.findAll('li'):
        try:
                a2 = li.contents[0].strip(" \t\n").decode('utf8')
                print "[http://" + a2+ "]"

                soup2 = BeautifulSoup.BeautifulSoup(urllib.urlopen("http://"+a2))
                try:
                        print unicode(soup2.head.title)
                except:
                        print soup2.head.title
        except:
                continue
```
<p><br></p>
<p>Na przykładzie widać najprostsze wyciąganie danych za pomocą <a href="http://www.python.org/">pythona</a> i biblioteki <a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup</a>.</p>
<p>Po delikatnym przeformatowaniu w npp można uzyskać coś takiego:</p>
<p><br></p>
<ul>
<li><a href="http://Gram.pl">http://Gram.pl</a> - gram.pl - Recenzje, Zapowiedzi, Newsy, Poradniki, Dema. Gry na PC, PS3, X360.</li>
<li><a href="http://Onepress.pl">http://Onepress.pl</a> - Księgarnia biznesowa Onepress.pl - książki klasy business</li>
<li><a href="http://Rebel.pl">http://Rebel.pl</a> - Sklep z grami REBEL.pl :: Największy polski sklep z grami - gry rpg, gry planszowe, gry karciane i inne</li>
<li><a href="http://Pixers.pl">http://Pixers.pl</a> - Fototapety, Obrazy na ścianę, Plakaty, Naklejki, Zdjęcia na płótnie - najciekawszy sklep w Europie - PIXERS</li>
<li>...</li>
</ul>
<p></p>
		