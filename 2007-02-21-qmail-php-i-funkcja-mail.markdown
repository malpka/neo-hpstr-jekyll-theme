---
layout: post
title: "qmail - php i funkcja mail()"
date: 2007-02-21 00:45
comments: true
categories:
- Linux
---
<p>Problem, który miałem ostatnio do rozwiązania wyglądał następująco:</p>
<p>W systemie domyślnym MTA jest qmail. po odebraniu wiadomości email wysłanej za pomocą funkcji mail() w skrypcie php, w treści listu widoczne są znaczniki html oraz nagłówki wiadomości.</p>
<p>Okazało się, że qmail nie jest do końca zgodny ze standardami RFC. W przypadku gdy standard wymaga stosowania do oddzielenia poszczególnych nagłówków znaków CRLF ( \r\n ) to on w przypadku linuxa, na którym się znajdował, oczekiwał linuksowego zakończenia linii LF ( \n ). Niestety w skryptach korzystających z mail() używane są przeważnie te pierwsze, co sprawia, że qmail w czasie analizy zamienia pierwszy \r na parę \r\n a co za tym idzie wprowadzając dający opisane wyżej nieciekawe rezultaty, ciąg \r\r\n.</p>
<p>przeszukując fora znalazłem sporo informacji na ten temat ale prawie żadnego sensownego rozwiązania. najbardziej przypadło mi do gustu to z postu <a href="http://bugs.php.net/bug.php?id=15841"></a></p>
<p><code>/etc/php.ini : sendmail_path = "unix2dos|dos2unix|sendmail -t -i"</code></p>
<p>Wszystko byłoby pięknie gdyby nie fakt, że do tej zmiennej w moim przypadku nie dało się wstawić potoków, musiałem więc zrobić to troszkę inaczej</p>
<p>stworzyłem dodatkowy skrypt:</p>
<p>/var/qmail/bin/sendmailfix<br>
<code>#!/bin/sh<br>
sed 's/^M$//' | /var/qmail/bin/sendmail ${1-@}</code></p>
<p>plik ten jest własnością grupy qmail chgrp qmail /var/qmail/bin/sendmailfix</p>
<p>teraz pozostaje jedynie dopisać ten skrypt jako ścieżka do programu sendmail i gotowe</p>
		