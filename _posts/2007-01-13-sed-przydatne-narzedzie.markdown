---
layout: post
title: "Sed - przydatne narzedzie"
date: 2007-01-13 01:14
comments: true
categories:
- Linux
---
<p>Czy kiedykolwiek zastanawiałeś się jak hurtem pozamieniać ciągi znaków w pliku? jeżeli chodzi nam o zwyczajny tekst to ostatecznie poradzi sobie z tym notatnik. Aby operować na znakach końca linii można wykorzystać Worda z pakietu Office. Jak jednak to zrobić najskuteczniej pod linuxem. Po zabawie z mcedit oraz vi doszedłem do wniosku ze oba mnie pod tym względem nie satysfakcjonują. Google poszło w ruch i naprowadziło mnie na świetne polecenie sed</p>
<p><b>sed</b> czyli Stream EDitor to edytor strumieniowy który znakomicie współpracuje z linuxowym bashem.</p>
<p>Moim zadaniem była dopisanie po kazdej linijce w pliku tekstowym nowej linijki jedynie za znakiem '-'</p>
<p>Dodanie po każdej linijce dodatkowej pustej linii</p>
<p><code>cat plik.txt | sed G &gt; plik.txt</code></p>
<p>Wypełnienie kazdej pustej linii znakiem '-'</p>
<p><code>cat plik.txt | sed "s/^$/-/" &gt; plik.txt</code></p>
<p>sed obsługuje przy wyszukiwaniu wyrażenia regularne.<br>
Zamiana ciągów znaków to dopiero początek góry lodowej ... <a href="http://www.student.northpark.edu/pemente/sed/sed1line.txt" class="external" rel="external">Sed w przykładach</a></p>
		