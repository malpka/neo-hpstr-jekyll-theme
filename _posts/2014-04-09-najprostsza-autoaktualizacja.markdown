---
layout: post
title: "Najprostsza instalacja i aktualizacja aplikacji skryptem bat"
date: 2014-04-09 07:43:53 +0200
comments: true
categories: 
---
Najprostszy schemat instalacji i autoaktualizacji aplikacji,
to pobranie najnowszej wersji przed uruchomieniem oraz umieszczanie plików w katalogu do których zalogowany użytkownik ma pełne uprawnienia.
W sieci lokalnej da się to zrealizować prostym skryptem batch.

Poniższy skrypt jest nawet bardziej 'inteligentny', gdyż za pomocą xcopy można kopiować jedynie nowsze pliki, 
co w znacznym stopniu ogranicza przesyłaną ilość danych i czas potrzebny na uruchomienie właściwej aplikacji.

``` bat
echo "App is starting, please wait..."

set targetdir=%APPDATA%/AppFolder
if not exist "%targetdir%" (
 mkdir "%targetdir%"
) 
xcopy \\192.168.0.1\SourceDir "%targetdir%" /E /D /C /Y
cd "%targetdir%"
App.exe
```


[xcopy](http://ss64.com/nt/xcopy.html).

- `/D` - kopiuje tylko te pliki, które mają nowszą datę modyfikacji  
- `/E` - kopiuje katalogi, również puste  
- `/C` - kontynuacja przy błędzie  
- `/Y` - automatyczne potwierdzanie nadpisania plików  
