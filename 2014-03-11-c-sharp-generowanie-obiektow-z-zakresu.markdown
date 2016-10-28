---
layout: post
title: "C# Generowanie obiektów z zakresu - Enumerable.Range()"
date: 2014-03-11 10:37:13 +0100
description: Tworzenie kolekcji obiektów na podstawie zdefiniowanego zakresu liczbowego - Enumerable.Range
comments: true
categories: C#
facebook:
    image: http://i.imgur.com/WURz5K4.png
---

{% img left http://i.imgur.com/WURz5K4.png 128 128 C Sharp %}

Czasami zachodzi potrzeba utworzenia kolekcji liczb/obiektów na podstawie zdefiniowanego zakresu liczbowego. 

Zamiast definiowania tablicy oraz używania pętli:

&nbsp; 


``` c#
public static List<YearClass> LoadData()
{
  List<YearClass> years = new List<YearClass>();
  for (int i = 2000; i < 2015; i++)
    years.Add(new YearClass(i));
  return years;
}
```

można wykorzystać `Enumerable.Range(int, int)` [link MSDN](http://msdn.microsoft.com/pl-pl/library/system.linq.enumerable.range%28v=vs.110%29.aspx)

``` c#
public static List<YearClass> LoadData()
{
 return Enumerable.Range(2000, 15).Select(x => new YearClass(x)).ToList<YearClass>();
}
```

Prawda że ładniej? Może nie jest to [itertools z Pythona](http://docs.python.org/2/library/itertools.html) ale robi to co trzeba.

Oczywiście metodę można wykorzystać do tworzenia różnego rodzaju ciągów:

``` c#
// ciąg arytmetyczny
var seq1 = Enumerable.Range(0, 5).Select(x => x * 3 + 2).ToList();
// 2, 5, 8, 11, 14

// kwadraty
var seq2 = Enumerable.Range(1, 6).Select(x => x * x).ToList();
// 1, 4, 9, 16, 25, 36

// potęgi dwójki
var seq3 = Enumerable.Range(0, 10).Select(x => (int)Math.Pow(2, x)).ToList();
// 1, 2, 4, 8, 16, 32, 64, 128, 256, 512
```

również znakowych:

``` c#
var percentStrArray = Enumerable.Range(0, 10).Select(x => (10 * x) + "%" ).ToArray();
// "0%", "10%", "20%", "30%", "40%", "50%", "60%", "70%", "80%", "90%"
```

Eksperymentalne pobieranie wszystkich małych liter ASCII wygląda następująco:
``` c#
var smallASCII = Enumerable.Range((int)'a', (int)'z' - (int)'a' + 1).Select(x => (char)x).ToArray();
// 'a', 'b', 'c', ..., 'y', 'z'
```
