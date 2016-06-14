---
layout: post
title: "Zapobieganie infekcjom wirusów - blokada autouruchamiania autorun.inf"
date: 2009-12-29 09:01
comments: true
categories:
- Do zapamiętania
- Ogólne
- Techblog
---
<p>Pod Windowsem najpewniejszym sposobem na zablokowanie automatycznego uruchamiania się nośników (CD/DVD, pendrive, dyski przenośne) podczas montowania lub podwójnego kliknięcia jest całkowite ignorowanie pliku <b>autorun.inf</b> następującym wpisem rejestru:</p>
<p><code>REGEDIT4 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\IniFileMapping\Autorun.inf] @="@SYS:DoesNotExist"</code></p>
<p>Należy skopiować powyższy tekst do pliku .reg (np. NoAutoRun.reg) i podwójnym kliknięciem scalić z rejestrem. Pozwoli to zapobiec jednemu z najczęściej obecnie występujących sposobów infekowania systemu.</p>
<p>Trzeba wziąć pod uwagę, że zablokowane zostanie też tworzenie kontekstowego menu oraz ikonki nośnika.</p>
<p>Wyjaśnienie dlaczego tak a nie inaczej oraz szczegółowy opis, zawierający zestawienie różnych metod blokowania <a href="http://www.publicsafety.gc.ca/prg/em/ccirc/2008/tr08-004-eng.aspx">tutaj</a>.</p>
<p>Sam długo używałem zmiany parametru "Zasady Komputer Lokalny/Konfiguracja komputera/Szablony administracyjne/System/Wyłącz funkcję Autoodtwarzanie" w zasadach grup (gpedit.msc), ale to nie powstrzymywało autoodtwarzania po podwójnym kliknięciu dla moich napędów.</p>
		