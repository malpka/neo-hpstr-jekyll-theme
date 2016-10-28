---
layout: post
title: "Przegląd darmowych hostingów obrazów - marzec 2014"
date: 2014-03-16 13:49:15 +0100
comments: true
categories: Octopress
facebook:
    image: http://blog.codemonkey.pl/images/hostingiobrazow.png
keywords: darmowy hosting obrazów, darmowy hosting zdjęć
description: Lista darmowych hostingów obrazów razem z ich parametrami - dostępną przestrzenią, limitem pliku, limitami transferu itp.
---

<!--
# Przegląd darmowych hostingów obrazów - marzec 2014#
-->
## Octopress - zamieszczanie obrazów we wpisie

{% img left /images/hostingiobrazow.png 250 250 hostingi %}

Jedną z uciążliwości [Octopress'a](http://octopress.org) jest sposób zamieszczania obrazków w postach - należy w poście podać bezpośredni url do obrazka (względny, w postaci `images/email.png`, lub bezwzględny: `http://blog.codemonkey.pl/favicon.png`).

Zgodnie z [dokumentacją img-tag](http://octopress.org/docs/plugins/image-tag/), ma to postać: 

<code>&#123;% img left http://x.pl/logo.png 220 92 logo %}</code>

Pierwszym sposobem jest umieszczenie obrazka w katalogu `source/images`, co po `rake deploy` skutkuje przeniesieniem _(git push / rsync)_ obrazka na hosting. Można się do niego odwołać względnym URLem. Drugim jest oczywiście hotlink do zewnętrznego serwisu.

Ponieważ nie chcę większymi zdjęciami zaśmiecać githuba, na którym hostowany jest blog, poświęciłem kilka chwil na poszukiwanie darmowego hostingu obrazków z przyzwoitymi warunkami.

Dodatkową motywacją do poszukiwań była zmiana polityki imageshack, która wprowadziła jedynie płatną usługę.

## Parametry brane pod uwagę

Najbardziej zwracałem uwagę na kilka cech: 

+ całkowity rozmiar dostępnej przestrzeni,
+ limit parametrów pojedynczego pliku (wielkość, wymiary, czas w przypadku filmów),
+ limit transferu,
+ wygasanie obrazków
+ możliwość uzyskania bezpośredniego odnośnika do zdjęcia
+ konieczność rejestracji
+ dostęp do API w celu automatycznego uploadu,
+ (łatwość dodawania zdjęć i pobierania bezpośredniego URLa do wstawienia przez stronę lub aplikację - istotne, ale często nie da się sprawdzić bez rejestracji)

Poniżej zamieściłem rezultaty krótkich poszukiwań. Zamieszczone dane są zebrane bezpośrednio ze stron hostingów, FAQ, itp...

## Charakterystyki darmowych hostingów obrazów

+ [Photobucket](http://photobucket.com/) [<sup>1<sup>](http://support.photobucket.com/hc/en-us/articles/200724044-Free-Accounts)[<sup>2</sup>](http://pic.photobucket.com/dev_help/WebHelpPublic/Content/FAQ/FAQOverview.htm) [<sup>3<sup>](http://pic.photobucket.com/dev_help/WebHelpPublic/Content/References/Limits.htm) {% img right http://www.baycitytxlib.org/ESW/Images/fa2431a139103530d007a353af5c4742.png 128 128 photobucket %}
  - 2 GB przestrzeni na obrazy i filmy poniżej 10min 
  - brak limitów parametrów zdjęć, film maks. 500 MB, 10 min, animowane gify do 5 MB i 800 ramek
  - 10 GB / miesiąc transferu
  - obrazy nie wygasają
  - API - dostępne, pewne ograniczenia dzienne, np 10 000 uploadów na dzień
  - konieczność rejestracji
+ [Flickr](https://www.flickr.com/) [<sup>4</sup>](https://www.flickr.com/help/limits/) (yahoo) {% img right http://increaserss.com/wp-content/uploads/flickr.png 128 128 flick %}
  - 1TB przestrzeni 
  - 200 MB / zdjęcie, 1 GB / film maks. 3 min
  - brak limitów transferu
  - obrazy nie wygasają
  - API dostępne
  - konieczność rejestracji
  - sporo aplikacji do zarządzania w [The App Garden](http://www.flickr.com/services/)
  - edit: jednak nie lubią hostować obrazków innych niż zdjęcia, ani być hotlinkowanym [link](https://www.flickr.com/guidelines.gne)
+ [imgur](http://imgur.com/) [<sup>5</sup>](http://imgur.com/faq) - używany na reddicie {% img right http://www.skylark95.com/wp-content/uploads/2012/04/Imgur_Logo_Icon_normal.png 128 128 imgur %}
  - brak limitu przestrzeni - obrazki są w serwisie dopóki mają 1 odsłonę w ciągu ostatnich 6 miesiecy
  - 10 MB / zdjecie, ale jeśli będzie powyżej 1 MB to zostanie przekompresowane do 1 MB (animowane do 2 MB)
  - rejestracja niewymagana, ale przydatna do zarządzania zdjęciami
  - API dostępne
  - 1 250 uploadów / dzień, ok. 12 500 pobrań / dzień
+ [TinyPic](http://tinypic.com/) [<sup>6</sup>](http://tinypic.com/faq.php) {% img right http://upload.wikimedia.org/wikipedia/en/5/58/TinyPic_logo.gif 103 37 tinypic %}
  - nieograniczona przestrzeń
  - maks. 1600 wymiaru, 100 MB, 5 min filmu
  - brak API
  - zdjęcia wyświetlane dopóki mają odsłony w ciągu ostatnich 90 dni
  - rejestracja niewymagana, ale ostatnio wprowadzili captchę
+ [Picasa](http://picasa.google.com/) [<sup>7</sup>](https://support.google.com/picasa/answer/43879?hl=en) [<sup>8</sup>](https://developers.google.com/picasa/docs/web_uploader#php_sample) {% img right http://www.muetasinfonia.org/img/hires/picasa_logo.png 128 128 picasa %}
  - 15 GB dostępne na wszystkich usługach google
  - pojedyncze zdjęcie maks. 50 MB, wideo 1 GB, maksymalnie 20 000 albumów, w każdym do 2 000 zdjęć
  - API dostępne
  - zdjęcia nie wygasają
  - uwagi: przy ręcznym dodawaniu zdjęć uciążliwe dostawanie się do linku bezpośredniego.
+ [fotosik.pl](http://fotosik.pl) [<sup>9</sup>](http://www.fotosik.pl/pomoc/faq/zagadnienia_ogolne/)
  - maksymalnie 100 zdjęć
  - 1,5 MB na zdjęcie
  - limit transferu: 1 GB miesięcznie
  - brak API
  - zdjęcia nie wygasają
  - rejestracja niewymagana
  
## Chmura

Sprawdziłem również jak hostingi typowo cloudowe radzą sobie z możliwością  hotlinkowania plików i obrazków bezpośrednio na stronie.

+ dropbox
  - 2 GB miejsca standardowo, możliwość powiększenia
  - trzeba [włączyć folder publiczny](https://www.dropbox.com/enable_public_folder)
+ box.com
  - direct link jedynie w wersji premium
+ mega.co.nz
  - nie ma możliwości otrzymania bezpośredniego URLa
+ OneDrive (SkyDrive)
  - nie ma możliwości otrzymania bezpośredniego URLa, jedynie kod z IFRAME

## Pozostałe, przejrzane ale niezbyt interesujące
+ <http://iv.pl> 
  - 1 MB na zdjęcie
  - bez logowania zdjęcia są usuwane po 14 dniach, po rejestracji - po 2 latach
+ <http://neepic.net>
  - 5 MB na obrazek
  - pliki kasowane po roku od ostatniego obejrzenia
+ <http://bayimg.com> - imagesharer od thepiratebay, minimum funkcjonalności.
+ <http://zapodaj.net> - strona, nawet najprostsze faq, działała tak wolno w trakcie otwierania że bałbym się zamieszczać tam zdjęcia;). Dodatkowo brak możliwości hotlinkowania, zdjęcia są usuwane po 3 miesiącach
+ <http://fotoo.pl> [<sup>info</sup>](http://fotoo.pl/service.php)
  - 50 MB przestrzeni
  - 2 MB na zdjęcie
  - 1 GB limitu / miesiąc.
+ <http://ifotos.pl>
  - 4 MB na zdjęcie
  - zdjęcia są usuwane jeśli w ciągu 3 miesięcy będą miały mniej niż 10 wizyt
  - mało informacji
+ <http://savepic.org> / <http://savepic.su> - język mnie skutecznie odstraszył;)
+ <http://www.garnek.pl>
  - "na konta można dodawać tylko własne zdjęcia"
  - "nie ma opłat ani limitów, byle nie wrzucać 5 tys. zdjęć dziennie"
+ <http://flog.pl> - usługa dedykowana na zdjęcia
+ <http://pixabay.com/> - zdjęcia umieszczane muszą spełniać [quality standards](http://pixabay.com/pl/blog/posts/photography-training-and-image-quality-standards-22/)
+ <http://www.imgland.net>
  - brak rejestracji
  - brak szczegółowych danych, ale niespotykane gdzie indziej rozpoznawanie użytkownika po IP

## Niesprawdzone

+ http://www.fotki.com/
+ http://www.ipernity.com/
+ http://www.pimpandhost.com
+ http://www.freeimagehosting.net/
+ http://postimage.org/
+ http://wstaw.org/
+ http://www.imagebam.com/
+ http://www.otofotki.pl/ - chętnie używane na chomiku

## Wnioski

Po sprawdzeniu wyżej wymienionych stron, porównując opisywane na nich parametry usługi z moimi oczekiwaniami, na czoło zdecydowanie wysuwa się Flickr, następnie Photobucket. 

Po rejestracji mamy możliwość kompletnego zarządzania kolekcją zdjęć, oraz pobierania bezpośredniego odnośnika do wstawienia na stronę. Oba hostingi dostarczają bardzo dużą przestrzeń do wykorzystania i racjonalne limity parametrów plików oraz transferu danych.

Ostateczną decyzję pewnie podejmę po zapoznaniu się z działaniem po rejestracji :)

## TODO

Aktualizacja w przyszłości, wrażenia po rejestracji, zebranie wyników w ładną tabelkę, opisanie pluginów do obsługi zewnętrznych serwisów [np takiego do flickr'a](https://github.com/neilk/octopress-flickr)
