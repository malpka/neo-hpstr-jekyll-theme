---
layout: post
title: "Zmiana firmware WRT54GL z Tomato na DD-WRT"
date: 2009-03-28 20:11
comments: true
categories:
- Ogólne
---
<p>Zdziwiło mnie, że aktualizacja oprogramowania przebiegła pomyślnie.</p>
<p>Mogło się nie udać na przykład z tego powodu że wersja DD-WRT którą wybrałem (dd-wrt.v24_vpn_generic.bin) zajmowała 3,52 MB, a Tomato raportował, że ilość pamięci dostępnej na cache'owanie procesu aktualizacji to około 2,1 MB</p>
<p>Na stronie DD wyczytałem, że czasami wymagane jest zainstalowanie najpierw wersji mini, dlatego przezornie ją pobrałem, ale ponieważ "jestem hardcorem" zainstalowałem od razu oprogramowanie docelowe.</p>
<p>Nie dość, że proces przeszedł pomyślnie, to okazało się że prawie wszystkie ustawienia zostały przywrócone. Chodzi tu m.in. o statyczne DHCP, konfigurację sieci bezprzewodowej - ssid, wep, ... . Jeszcze muszę poszukać gdzie jest przekierowanie portów.</p>
<p>Na DD-WRT przeszedłem, bo potrzebny mi VPN, ale też chciałem zobaczyć jak wygląda coś innego niż domyślne oprogramowanie oraz Tomato.</p>
<p>Jedyne, co mnie zirytowało to polskie tłumaczenie, często pomieszane z angielskim, albo wplecione w angielski szyk zdania. Szybko przełączyłem się na eng;)</p>
<p>Wielkie podziękowania za tak sprawnie działający firmware dla twórców!</p>
<p></p>
<p>--------- Edit 29.03.2009</p>
<p>W nowym oprogramowaniu umieszczenie funkcji jest mniej intuicyjne niż w poprzednim. Myślałem że to kwestia przyzwyczajenia, ale po tych 2 dniach zabawy nadal ciężko mi znaleźć opcję której szukam.<br>
Jednak konfiguracja przekierowania portów się nie zachowała.</p>
		