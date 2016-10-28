---
layout: post
title: "Windows - uruchamianie skryptu bat / cmd jako administrator - problem aktualnej ścieżki wywołania"
date: 2014-04-06 15:47:03 +0200
comments: true
facebook:
    image: http://i.imgur.com/mNHnpU9.png
---

{% img left http://i.imgur.com/mNHnpU9.png 256 256 cmd %}


W nowych wersjach systemu Windows (8 i 8.1 na pewno, we wcześniejszych nie testowałem) zmienił się katalog wywołania skryptów uruchamianych jako administrator.
Domyślnie zamiast katalogu bieżącego jest to:

`%SYSTEM%`

czyli na przykład
 
`C:\Windows\system32`

Aby przywrócić funkcjonalność starych skryptów można zastosować na początku  przejście do katalogu wywołania:

```
    setlocal enableextensions
    @cd /d "%~dp0"
```

gdzie:


`@setlocal enableextensions` - [umożliwia dostęp do rozszerzenia CMD](http://ss64.com/nt/setlocal.html)

Ponieważ:  `%0` to pełna ścieżka do wywoływanego programu (skryptu)

to:

`@cd /d "%~dp0"` - przejście do katalogu wywołania, wykorzystujące [dodatkowe zmienne skryptowe](http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/percent.mspx?mfr=true)

`%0` to standardowo nazwa pliku (skryptu) wykonywalnego wraz ze ścieżką, a `~dp` wyciągnięcie z niej litery dysku oraz samej ścieżki do katalogu.

[Źródło](http://www.codeproject.com/Tips/119828/Running-a-bat-file-as-administrator-Correcting-cur)
