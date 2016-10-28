---
layout: post
title: "Octopress zamiast Wordpressa - statyczna generacja bloga"
date: 2014-02-11 21:16:45 +0100
comments: true
categories: octopress
facebook:
    image: http://www.byzantinereality.com/images/octopress.png

---

Obecnie rozpoczęcie blogowania nie nastręcza wielu trudności - trzeba zdecydować się na jedną z platform blogowych, jak Blogger czy Wordpress.com, poświęcić chwilkę na konfigurację oraz wybranie skórki i można zacząć pisać. To wystarcza w zupełności do dzielenia się ze społecznością internetową swoimi przemyśleniami, nawet zespołowo.

W przypadku gdy możliwości platformy przestają wystarczać, reklamy dokuczać, zasięg i poczytność bloga zwiększają się czy w planach jest komercyjne wykorzystanie tworzonych treści, wymagające odpowiedniego zastosowania SEO czy statystyk użytkowników piszący zazwyczaj decyduje się na przejście "na swoje": wykupienie domeny, hostingu z PHP i MySQL oraz postawieniu na nim silnika - tu nikogo nie zaskoczę - **Wordrpress.org**.

## Wordpress ##

Standardowa zautomatyzowana instalacja: "ZACZYNAMY", baza nazwa, hasło, użytkownik, prefiks, DALEJ, tytuł witryny, użytkownik, hasło, mail, DALEJ, logowanie ... i co, to już? Gdzie tu zabawa, gdzie konfiguracja, ile razy można? ;-)

Przy wyborze swojego miejsca do notowania zacząłem oczywiście od wyszukania rozwiązań alternatywnych i niebanalnych, co pozwoliło mi trafić na zupełnie inne podejście do generowania blogów.

Zacznijmy może od pytania:

### Z czego składa się blog? ###

Pytanie proste, odpowiedź raczej też, ale ma znaczenie przy dalszych rozważaniach. Przy opisie będę się opierał na WP.

1. **Wpisy**
   - tytuł
   - data wpisu (na jej podstawie tworzone jest archiwum / kalendarium bloga)
   - treść (tekst, obrazki)
   - kategoria (przekłada się na listę kategorii z odnośnikami do wpisów)
   - tagi (j.w.)
2. **Strony**
3. **Komentarze do wpisów**
4. **Menu**
5. _Motyw wyglądu_
6. _Inne treści - widgety_
7. _Panel konfiguracyjny_ 

Pogrubieniem zaznaczyłem pozycje istotne z punktu widzenia samej treści bloga.

Biorąc teraz pod uwagę, że Wordpress to skrypty PHP i leżąca pod spodem baza danych można zadać drugie pytanie:

### Jak działa Wordpress? ###

Jeden prosty `GET / HTTP/1.0` do pojedynczego wpisu na blogu opartym na WP to szereg zdarzeń na hostingu, będących w rzeczywistości wykonaniem skryptów PHP, pobieraniem danych z MySQLa oraz prezentacji wyników jako stronę WWW.

* wczytanie konfiguracji
* połączenie PHP do bazy z zapytaniem o strukturę Menu i wyświetlenie jej
* pobranie z MySQLa listy zazwyczaj 3-5+ wpisów, ucinanie do `<!-- more -->`
* pobranie listy kategorii z countami po liczbie wpisów,
* PHP -> MySQL -> `select * from wp_comments where comment_post_ID = ...`
* ... itd

Sporo kodu, zapytań bazodanowych jedynie po to by pobrać statyczną treść jednego wpisu, trochę więcej zmieniające się komentarze i kilku informacji dodatkowych.

A przecież zawartość tych struktur, oraz strony, na jakie mają wpływ, zmienia się **tylko podczas dodawania wpisu**, a komentarze przeważnie w pewnym zakresie czasu od daty publikacji. Dodatkowo sporo osób decyduje się na wprowadzenie [Disqus](http://disqus.com/) czy FB jako osobnego silnika komentarzy.

Dla bloga, na którym wpis pojawia się raz dziennie, oraz który odwiedza w ciągu tego jednego dnia 100 użytkowników to **aż 99 niepotrzebnych** przegenerowań stron na dzień.

### Przyspieszanie Wordpressa - unikanie zbędnej generacji stron ###

Oczywiście WP jako dojrzała platforma blogowa, która obsługuje w niektórych przypadkach pewnie i setki tysięcy żądań na dzień posiada [zalecenia](http://codex.wordpress.org/WordPress_Optimization/Caching) dotyczące wydajności, które zawierają m.in.

* instalację pluginów cache'ujących - W3 Total Cache czy WP Super Cache 
* cache w przeglądarkach klientów, przydatne dla powracających (HTTP Cache-Control)
* cache po stronie serwera: Varnish, Reverse proxy, Alternative PHP Cache (APC)

jednak rozwiązania takie dalej bazują na PHP i danych w bazie i są zależne od wydajności hostingu.

## Alternatywa - statyczne generowanie stron ##

Konkurencyjny pomysł jest prosty - zamiast ciągłego przetwarzania PHP + MySQL można przegenerować bloga lub inną stronę w trakcie dodawania treści. Silnik generacji, uzupełniony o szablony struktury , wyglądu (CSS), zapisana w umówionym formacie treść oraz komentarze w zewnętrznym serwisie typu Disqus to wszystko co trzeba aby stworzyć w pełni funkcjonalnego bloga. _Unikamy oczywiście drastycznego pomysłu ręcznego dodawania strony html ;)_

<a href="http://jekyllrb.com/">{% img right http://jekyllrb.com/img/logo-2x.png 249 115 Jekyll logo %}</a>

### Jekyll ###


Przykładem tego podejścia jest [Jekyll](http://jekyllrb.com/), napisany w ruby zestaw generatorów oraz skryptów wykonujących całą brudną robotę.


Cechy generatora to, cytując stronę:

* prostota - _"bez baz danych, moderacji komentarzy ani nieznośnych aktualizacji - tylko Twoja treść"_
* statyczność - _"[Markdown](http://daringfireball.net/projects/markdown/) (lub [Textile](http://textile.sitemonks.com/)) jako format wpisów, [Liquid](http://wiki.shopify.com/Liquid) jako silnik szablonów, HTML & CSS. Wyjściem generacji są statyczne witryny gotowe do publikacji."_
* przygotowany pod blogi - _"permalinki, kategorie, strony, wpisy, własne motywy."_

Projekt jest bardzo dobrze udokumentowany, strona prezentuje się bardzo przyjemnie i tłumaczy krok po kroku w instalację oraz sposób publikacji treści.

Quickstart jest imponująco krótki:

``` bash
~ $ gem install jekyll
~ $ jekyll new myblog
~ $ cd myblog
~/myblog $ jekyll serve
# => Now browse to http://localhost:4000
```

i już można podziwiać działającą stronę. 

To oczywiście dopiero początek, pozostała praca przy szablonie wizualnym bloga w Liquid.

Same posty to pliki w katalogu `_posts` o nazwie w postaci `YEAR-MONTH-DAY-title.MARKUP`, np:

```
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile
```

Tekst piszemy w Markdown lub Textile, dokładając na początku pliku [YAML-owy nagłówek](http://jekyllrb.com/docs/frontmatter/) zawierający np. kategorie, tagi i inne informacje dodatkowe. Zawsze można dorzucić fragment HTMLa.


<a href="http://octopress.org">{% img right http://octopress.org/images/logo.png 227 227 Octopress logo %}</a>

### Jeszcze szybszy start - Octopress ###

Aby jeszcze bardziej ułatwić tworzenie nowego bloga na bazie Jekylla powstał framework zawierający gotową konfigurację, skrypty, szablony wizualne i kod w Javascripcie - [Octopress](http://octopress.org)


_Out of the box_ mamy:

* Gotowy szablon HTML5,
* Zorientowany na platformy mobilne "responsywny" layout,
* Wbudowane wsparcie dla Twittera, Google Plus One, komentarzy Disqus, Pinboarda, Delicious, oraz Google Analytics,
* Łatwe wdrażanie przy użyciu Github pages lub Rsync,
* Wsparcie dla serwerów POW and Rack dla podglądu wyników pracy,
* Proste szablony wizualne - Compass i Sass
* Podświetlanie składni kodu - [Solarized](http://ethanschoonover.com/solarized)

Dodatkowo sporo wtyczek zewnętrznych oraz aktywność społeczności.

Po instalacji:

``` bash
	$ git clone git://github.com/imathis/octopress.git octopress
	$ cd octopress 
	# gem install bundler
	# rbenv rehash # If you use rbenv, rehash to be able to run the bundle command
	# bundle install 
	$ rake install
```
[konfigurujemy deployment](http://octopress.org/docs/deploying/) na Githubie, Heroku lub rsync-em, [główne parametry bloga](http://octopress.org/docs/configuring/) jak tytuł, tagi meta, rss itp. oraz dodajemy treść:

``` bash
	$ rake new_post["Octopress zamiast Wordpressa"]
	mkdir -p source/_posts
	Creating new post: source/_posts/2014-02-11-octopress-zamiast-wordpressa.markdown
```

```
	---
	layout: post
	title: "Octopress zamiast Wordpressa - statyczna generacja bloga"
	date: 2014-02-11 21:20
	comments: true
	categories: Octopress
	--- 
	# Octopress zamiast Wordpressa - statyczna generacja bloga 
	
	## Blogowanie dziś  

	Obecnie rozpoczęcie blogowania nie nastręcza wielu trudności ... 
```

Generujemy stronę oraz uruchamiamy serwer testowy, domyślnie na porcie 4000

``` bash
	$ rake generate && rake preview
```

Ostatecznie publikujemy wcześniej skonfigurowanym mechanizmem:

``` bash
	$ rake deploy
```

Polecam zapoznanie się z wygenerowaną strukturą stron na [https://github.com/malpka/malpka.github.io](https://github.com/malpka/malpka.github.io)

### Alternatywy

Statyczne generatory stron to temat rozległy, wystarczy spojrzeć na stronę [http://staticsitegenerators.net/](http://staticsitegenerators.net/), gdzie obecnie jest 224 wpisów. Ciągle pojawiają się nowe, jak np [http://jekyllbootstrap.com](http://jekyllbootstrap.com) v0.2 na który trafiłem podczas pisania.


## Podsumowanie ##

### Zalety ###

* statyczne generowanie stron - przeważnie raz na wpis &rarr; szybkość działania,
* posiada wszystkie ważne funkcje bloga: wpisy, strony, komentarze, tagi, kategorie, permalinki
* nie wymaga hostingu z PHP i MySQL,
* wbudowane publikowanie np. na darmowych github pages, do których można podłączyć swoją domenę,
* uniezależnienie się od Wordpressa _(bo ileż można?)_,
* na prawdę proste zamieszczanie kodu źródłowego który dodatkowo ładnie wygląda,
* szybkie pisanie postów na konsoli: `rake new_post["tytuł wpisu"]` + treść w Markdown/Textile
* możliwość automatyzacji - np. posty przez maila, posty na bazie innej strony.

### Wady ###

* wymagana większa wiedza techniczna _(ale w końcu to "blogging framework for hackers.")_,
* konieczność przygotowania środowiska w ruby dla samego generatora,
* konieczność stworzenia własnego szablonu, dostępnych jest kilkadziesiąt(set), w porównaniu do kilku(dziesięciu) tysięcy na WP
* nie ma wygodnego panelu administracyjnego, posty edytujemy jako pliki
* brak wygodnego zamieszczania zdjęć, trzeba dodać [link bezpośredni](http://octopress.org/docs/plugins/image-tag/)
* odrębny mechanizm komentarzy - Disqus
