---
layout: post
title: "Debian - dodawanie usług uruchamianych podczas startu"
date: 2007-01-12 18:35
comments: true
categories:
- Ogólne
---
<p>Prosty skrypt konfiguracji sieci bezprzewodowej</p>
<p><code>echo '#!/bin/bash' &gt; /etc/init.d/wlanstart<br>
echo 'iwconfig wlan0 essid malpka mode Ad-Hoc channel 11' &gt;&gt; /etc/init.d/wlanstart<br>
chmod +x /etc/init.d/wlanstart<br>
update-rc.d wlanstart defaults</code></p>
<p>Serwer mi padł po 7 dniach uptime bo w gniazdku zaczęło mi się iskrzyć. Już naprawione, ale po podniesieniu się systemu wlan nie działał i internetu w całym domu nie miałem .. straszne.</p>
<p>edit:<br>
Poprawka .. kod ustawiający wlan nie powinien być wrzucony do init.d ale do /etc/network/interfaces<br>
Do konfiguracji interesującego nas interfejsu należy dopisać:</p>
<p><code>up /usr/local/bin/wlanstart</code></p>
		