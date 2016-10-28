---
layout: post
title: "MPlayer - Instalacja kodeków rmvb (i nie tylko) pod linuksem"
date: 2010-03-09 17:46
comments: true
categories:
- Do zapamiętania
- Linux
---
<p></p>
<pre>
cd ~<br>wget http://www1.mplayerhq.hu/MPlayer/releases/codecs/all-20061022.tar.bz2<br>sudo mkdir /usr/lib/codecs<br>sudo ln -s /usr/lib/codecs /usr/lib/codecs-win32<br>tar jxvf all-20061022.tar.bz2<br>sudo mv all-20061022/* /usr/lib/codecs<br><br>wget http://www1.mplayerhq.hu/MPlayer/releases/codecs/rp9codecs-20050115.tar.bz2<br>sudo mkdir /usr/lib/real<br>tar jxvf rp9codecs-20050115.tar.bz2<br>sudo mv rp9codecs-20050115/* /usr/lib/real
</pre>
<p>