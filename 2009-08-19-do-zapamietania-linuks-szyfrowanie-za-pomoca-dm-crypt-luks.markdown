---
layout: post
title: "Do zapamiętania: Linuks - szyfrowanie za pomocą dm-crypt / luks"
date: 2009-08-19 07:56
comments: true
categories:
- Do zapamiętania
- Linux
---
<p>Zacząłęm to pisać sam, nawet już z pamięci, ale znalazłem <a href="http://mlawire.blogspot.com/2009/07/encrypted-filesystem-on-loop-device.html">stronę</a> na której jest dokładnie to co chciałem. Nie lubię korzystać w taki sposób z czyjejś pracy ale tym razem to będzie prywatnie dla mnie do zapamiętania.</p>
<p><code>modprobe dm_mod</code></p>
<h3>Tworzenie zaszyfrowanego systemu plików:</h3>
<p><code># create a 10M file<br>
$ dd if=/dev/urandom of=testfs bs=1M count=10<br>
<br>
# associate it with the loop device<br>
$ losetup /dev/loop0 testfs<br>
<br>
# encrypt it (will ask for password to use)<br>
$ cryptsetup luksFormat /dev/loop0<br>
<br>
# open the encrypted loop device<br>
$ cryptsetup luksOpen /dev/loop0 testfs<br>
<br>
# format it with ext2 (or whatever you prefer)<br>
$ mkfs.ext2 /dev/mapper/testfs<br>
<br>
# mount it<br>
$ mount /dev/mapper/testfs /mnt/test<br>
<br>
# confirm mount<br>
$ df -h /mnt/test<br>
Filesystem Size Used Avail Use% Mounted on<br>
/dev/mapper/testfs 9.2M 88K 8.7M 1% /mnt/test</code></p>
<h3>Odmontowanie systemu plików:</h3>
<p><code># unmount it<br>
$ umount /mnt/test<br>
<br>
# close encryption<br>
$ cryptsetup luksClose /dev/mapper/testfs<br>
<br>
# release loop device<br>
$ losetup -d /dev/loop0</code></p>
<h3>Montowanie szyfrowanego systemu plików:</h3>
<p><code><br>
# associate file with the loop device<br>
$ losetup /dev/loop0 testfs<br>
<br>
# open the encrypted loop device<br>
$ cryptsetup luksOpen /dev/loop0 testfs<br>
<br>
# mount it<br>
$ mount /dev/mapper/testfs /mnt/test<br></code></p>
		