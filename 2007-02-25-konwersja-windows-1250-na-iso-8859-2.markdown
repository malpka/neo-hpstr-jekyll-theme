---
layout: post
title: "Konwersja znaków z Windows-1250 na ISO-8859-2 (i inne UTF-8 'y)"
date: 2007-02-25 17:44
comments: true
categories:
- Linux
---
Konwersja stron kodowych, wszystko za pomocą linuksowego `iconv`, który [jest również dostępny dla Windows](http://gnuwin32.sourceforge.net/packages/libiconv.htm):

Najprościej zrobić to po prostu podając kodowanie docelowe

```
iconv -t UTF-8 plik_wejsciowy.txt > plik_wyjsciowy.txt
```

ale można również wymusić


## Zamiana ISO-8859-2 na Windows-1250
```
iconv -f CP1250 -t ISO8859-2 plik_cp1250.txt &gt; plik_iso8859-2.txt
```

## Zamiana Windows-1250 na ISO-8859-2
```
iconv -f ISO8859-2 -t CP1250 plik_iso8859-2.txt &gt; plik_cp1250.txt
```

## Zamiana ISO-8859-2 na UTF-8
```
iconv -f CP1250 -t UTF-8 plik_cp1250.txt &gt; plik_utf-8.txt
```

## Zamiana Windows-1250 na UTF-8
```
iconv -f ISO8859-2 -t UTF-8 plik_iso8859-2.txt &gt; plik_utf-8.txt
```


