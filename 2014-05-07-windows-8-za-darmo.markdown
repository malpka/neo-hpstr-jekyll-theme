---
layout: post
title: "Windows 8 (i nie tylko) za darmo"
date: 2014-05-07 21:38:49 +0200
comments: true
categories: lifehacking
facebook:
    image: http://blog.codemonkey.pl/images/windows-8-logo.jpg
---
{% img left /images/windows-8-logo.jpg 280 200 windows-8-logo %}


Oprócz świetnych warunków licencyjnych Dreamspark dla studentów, Microsoft oferuje także możliwość przetestowania niektórych produktów. 
W prosty sposób można mieć legalny system operacyjny z **pewnego źródła**, na stosunkowo długi czas - od 90 nawet do 240 dni, z dostępem do aktualizacji.

Z zamieszczonych poniżej linków można pobrać obrazy iso. Posiadają one zintegrowany klucz, nie jest on wymagany podczas instalacji.

<!-- more -->

Każdy z systemów posiada pewien czas, ang. *initial grace period*, w trakcie którego należy dokonać aktywacji. Okres ten może zostać ponowiony (w przypadku Windows Server 2008 R2 nawet pięciokrotnie) poleceniem `slmgr.vbs -rearm`. 

Status aktywacji można sprawdzić przez `slmgr.vbs -dli`

{% img center /images/slmgr_vbs-dli.png 350 217 slmgr_vbs-dli %}


Po aktywacji dostępny jest czas na testy, odpowiednio dla systemów serwerowych 180 dni, dla Windows 8 - 90 dni. Po upływie wspomnianego okresu tło zmieni się na czarne a komputer będzie wyłączał się co godzinę uniemożliwiając pracę ;).


Poniżej lista najciekawszych na chwilę obecną propozycji.

## Windows 8.1 za darmo

- Windows 8.1 Enterprise Evaluation 
- http://technet.microsoft.com/en-US/evalcenter/hh699156.aspx
- Konieczna rejestracja do pobrania obrazu.
- Czas pracy: 10 dni (initial grace period) + 90 dni = **100 dni**
- Aktywacja najpóźniej do 31 paźniernika 2014!

## Windows Server 2012 R2

- Konieczna rejestracja do pobrania obrazu.
- http://technet.microsoft.com/en-US/evalcenter/dn205286
- Czas pracy: X (mało informacji na ten temat) * 10 dni + 180 dni = minimum **190 dni**
- Konfiguracja jako workstation - http://www.win2012workstation.com/

## Windows Server 2008 R2

- http://www.microsoft.com/en-us/download/details.aspx?id=11093
- Czas pracy: 6  * 10 dni + 180 dni = **240 dni**

Najpopularniejszy, z systemów, dobrze opisany, np [tutaj](http://www.win2008r2workstation.com/), [lista sprawdzonych gier 2008](http://www.win2008workstation.com/games-and-entertainment/)


## Wady 

Oczywiście nie jest aż tak różowo. Oprócz konieczności reinstalacji systemu po 100 - 240 dniach, wspomniane systemy są dostępne jedynie w ograniczonej liczbie języków (brak polskiego). W przypadku rozwiązań serwerowych należy poświęcić trochę czasu na dopasowanie systemu do komputera użytkowego ;). 
Niektóre z programów nie są kompatbilne z wersjami serwerowymi (przykład: Easeus Partition Manager, niektóre gry).
Sterowniki do karty graficznej posiadają przynajmniej w moim przypadku (MSI R6870) znacznie mniej ustawień - nie mogę dopasować sygnału HDMI idącego do odbiornika (przykład - Overscan)

## Zalety

Poza wymienionymi wcześniej - działają gry od Blizzarda - Diablo 3, Heartstone, działa Injustice, działa Steam ;)

<a href="http://imgur.com/1T0Xook" target="_blank"><img src="http://i.imgur.com/1T0Xook.png" title="Hosted by imgur.com" /></a>


