---
layout: post
title: "Automatyczna zamiana nazw plików i zawartości"
date: 2009-10-23 12:20
comments: true
categories:
- Do zapamiętania
- Programowanie
---
<p>Sytuacja z życia, rozwiązanie do zapamiętania. Bazując na starym projekcje o określonym nazewnictwie plików oraz klas, namespace itd. trzeba stworzyć nowy z całkowicie zmienioną jedną frazą na drugą.</p>
<p>Rozwiązanie</p>
<p>Zamiana zawartości:</p>
<p><code>grep -rl NazwaPierwotna . | xargs sed -i -e 's/NazwaPierwotna/NazwaDocelowa/g'</code></p>
<p>Zmiana nazw plików</p>
<p><code>find . -name "NazwaPierwotna*" -exec rename 's/NazwaPierwotna/NazwaDocelowa/' {} \;</code></p>
<p>To ostatnie wywołać kilka razy</p>
		