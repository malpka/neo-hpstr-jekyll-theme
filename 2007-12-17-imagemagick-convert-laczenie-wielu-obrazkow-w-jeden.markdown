---
layout: post
title: "ImageMagick convert - łączenie wielu obrazków w jeden"
date: 2007-12-17 18:53
comments: true
categories:
- Linux
---
<p>Wybierając się do Zakopanego pomyślałem, że przydałaby się mapa tego miejsca. Nie chcąc dać zarobić tym $%^ wyzyskiwaczom (:P) pomyślałem że znajdę sobie mapkę na necie</p>
<p>Szybka akcja w stylu google.pl?q=zakopane+mapa doprowadziła mnie do strony:</p>
<p><a href="http://www.mapytatr.net/PRODUKTY/MAPY_TAT/ZAKOPANE/SLICES/zkp_iii.html">http://www.mapytatr.net/PRODUKTY/MAPY_TAT/ZAKOPANE/SLICES/zkp_iii.html</a></p>
<p>zapisałem na dysku, jednak doszedłem do wniosku, że lepiej będzie się ją obrabiało gdy będzie w pojedynczym pliku. Parę machnięć w Gimpie i doszedłem do wniosku że nie tędy droga. Przypomniałem sobie że na serwerze mam zainstalowane imagemagick, więc spróbowałem pójść tędy.</p>
<p>Początkowa wersja:</p>
<p><code>convert +append zkp_01.jpg zkp_02.jpg (...) a.ppm<br>
convert +append zkp_10.jpg zkp_11.jpg (...) b.ppm</code></p>
<p>Cóż, już lepiej, wszystko dzieje się automatycznie, ale nadal czegoś brakuje. Spróbowałem wildcharów / regexpów i okazało się, że poprawna jest konstrukcja:</p>
<p><code>convert +append zkp_1[0-8].jpg b.ppm</code></p>
<p>Zatem ostatecznie:</p>
<p><code>convert +append zkp_0[1-9].jpg a.ppm<br>
convert +append zkp_1[0-8].jpg b.ppm<br>
convert +append zkp_19.jpg zkp_2[0-7].jpg c.ppm<br>
convert +append zkp_2[8-9].jpg zkp_3[0-6].jpg d.ppm<br>
convert +append zkp_3[7-9].jpg zkp_4[0-5].jpg e.ppm<br>
convert +append zkp_4[6-9].jpg zkp_5[0-4].jpg f.ppm<br>
convert +append zkp_5[5-9].jpg zkp_6[0-3].jpg g.ppm<br>
convert +append zkp_6[4-9].jpg zkp_7[0-2].jpg h.ppm<br>
convert +append [a-h].ppm mapa.jpg</code></p>
		