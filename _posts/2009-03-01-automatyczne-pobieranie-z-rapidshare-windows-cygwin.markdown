---
layout: post
title: "Automatyczne pobieranie z Rapidshare na Windowsie z wykorzystaniem Cygwina."
date: 2009-03-01 14:39
comments: true
categories:
- Linux
- Techblog
---
<p>Jeżeli jesteś osobą korzystającą serwisu Rapidshare pewnie Twoja zabawa z nim wygląda następująco:</p>
<ul>
<li>klikasz na link / wklejasz jako adres w przeglądarce</li>
<li>Naciskasz przycisk "Free User"</li>
<li>Niecierpliwie czekasz aż cyferki dojdą do zera, a następnie znowu klikasz w przycisk Download.</li>
</ul>
<p>O ile w przypadku pojedynczych plików da się to zaakceptować, to gdy jest do pobrania kilkadziesiąt części nazwanych part[0-9]+.rar dochodzi problem oczekiwania do 30 minut między pobieraniem, oraz konieczność kontrolowania całego procesu pobierania i powtarzania wyżej wspomnianych kroków (stan na dzień 2009-03-01).</p>
<EXCERPT><p>Użytkownicy systemów *nixowych mają od jakiegoś czasu możliwość skorzystania ze znakomitego i cały czas uaktualnianego skryptu rsget-mod którego autorem jest <a href="nerdblog.pl">d4rky</a></p>
<p><a href="http://rs.nerdblog.pl/">rsget-mod - strona projektu</a></p>
<p>Skrypt umożliwia pełną automatyzację procesu pobierania zarówno pojedynczego linku, jak i zbioru adresów zapisanych w pliku.</p>
<p>Jeżeli jesteś użytkownikiem Windowsa ... cóż, najpierw chociaż wypróbuj Linuxa ;), a jeśli dojdziesz do wniosku, że Ci nie odpowiada, możesz skorzystać z Cygwina, który jest linuksopodobnym środowiskiem działającym pod kontrolą systemu Microsoftu, emulującym funkcje API Linuxa.</p>
<p><a href="http://www.cygwin.com/">Oficjalna strona projektu Cygwin</a></p>
<p>Instalacja jest intuicyjna, ale aby przyszłe wersje skryptu były obsługiwane warto zatrzymać się przy wyborze pakietów i upewnić się, że będą instalowane:</p>
<p></p>
<ul>
<li>Base / grep</li>
<li>Net / wget</li>
<li>Net / curl</li>
</ul>
<p></p>
<p><img src="http://i40.tinypic.com/2ciei3l.jpg"></p>
<p>Po zakończeniu instalacji można już uruchomić środowisko, które powita nas ślicznym promptem.</p>
<p><img src="http://i44.tinypic.com/s3q25v.jpg"></p>
<p>Cygwin to dobre środowisko dla osób, które chcą rozpocząć przygodę z linuxem, bądź wykorzystać jego zalety, m.in. jak w naszym przypadku możliwości skryptowe. Jednak nic nie stoi na przeszkodzie, aby emulować również środowisko graficzne za pomocą <a href="http://kde-cygwin.sourceforge.net/">Kde on Cygwin</a></p>
<p>Wróćmy jednak do tematu. Skrypt wymaga kilku kroków przygotowawczych. Wygodniej będzie na przykład umieścić go w katalogu dostępnym przez zmienną PATH, by uprościć jego wywoływanie. Ponadto należy mu nadać atrybut wykonywalności.</p>
<p><code>cd /usr/local/bin<br>
wget http://rs.nerdblog.pl/stable/latest/rsget-mod.sh<br>
chmod +x rsget-mod.sh</code></p>
<p>Uwaga! W przypadku korzystania z serwera proxy należy wcześniej ustawić zmienną http_proxy:</p>
<p><code>export http_proxy="http://adres_serwera:port/"</code></p>
<p>lub</p>
<p><code>export http_proxy="http://użytkownik:hasło@adres_serwera:port/"</code></p>
<p>Sprawdzamy czy wszystko jest tam, gdzie trzeba i wywołujemy skrypt po raz pierwszy.</p>
<p><img src="http://i42.tinypic.com/28c2hs2.jpg"></p>
<p>Wersja unstable stworzy dodatkowo w katalogu domowym użytkownika swój podkatalog z ustawieniami oraz plikami pomocniczymi.</p>
<p>Teraz wystarczy jedynie nakarmić skrypt linkami do pobierania:</p>
<p><code>cat &gt; ~/linki.txt<br>
http://rs123.rapidshare.com/files/1234567891/BigFile_part1.rar<br>
http://rs123.rapidshare.com/files/1234567892/BigFile_part2.rar<br>
http://rs123.rapidshare.com/files/1234567893/BigFile_part2.rar<br>
[Ctrl+D]</code></p>
<p>Inicjujemy ściąganie za pomocą</p>
<p><code>rsget-mod.sh ~/linki.txt</code></p>
<p><img src="http://i44.tinypic.com/332xo2o.jpg"></p>
<p><img src="http://i40.tinypic.com/1055p51.jpg"></p>
<p>Od teraz skrypt zajmie się wszystkimi czynnościami związanymi z obsługa pobierania i oczekiwania. Nam pozostaje tylko zostawić maszynę i wybrać się na spacer lub wycieczkę rowerową.</p>
		