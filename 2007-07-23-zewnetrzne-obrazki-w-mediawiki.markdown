---
layout: post
title: "Zewnętrzne obrazki w MediaWiki"
date: 2007-07-23 11:58
comments: true
categories:
- Ogólne
---
<p>Domyślnie w nowych wersjach MediaWiki dodanie linku do zewnętrznego obrazka powoduje, że widoczny jest jedynie jego adres. Aby umożliwić "hotlinkowanie", czyli faktyczne wstawienie grafiki na stronę, należy dopisać w pliku konfiguracyjnym <b>LocalSettings.php</b> linię:<br>
<code>$wgAllowExternalImages = true;</code></p>
		