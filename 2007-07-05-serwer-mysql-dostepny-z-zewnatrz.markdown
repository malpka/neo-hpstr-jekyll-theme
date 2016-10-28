---
layout: post
title: "Serwer MySQL dostępny z zewnątrz"
date: 2007-07-05 11:35
comments: true
categories:
- Linux
---
<p>Uczę się obecnie Hibernate i podczas pisania najprostszego programu który operował na pojedynczej tabeli wystąpił błąd połączenia z bazą danych</p>
<p>Przy korzystaniu ze standardowego connectora do bazy po sieci lokalnej:<br>
<code>jdbc:mysql://10.0.1.4:3306/quiz</code><br>
odezwał się exception o braku możliwości połączenia z bazą, mimo że była ona skonfigurowana poprawnie i normalne wykorzystywanie jej jako wsparcie la apache odbywało się bez problemów</p>
<p>Okazuje się że MySQL jest na tyle restrykcyjny przy instalacji, że zabrania połączenia z adresów innych niż localhost.</p>
<p>Aby to zmienić należy w pliku <b>/etc/mysql/my.cnf</b> zakomentarzować dyrektywę <b>skip-networking</b></p>
		