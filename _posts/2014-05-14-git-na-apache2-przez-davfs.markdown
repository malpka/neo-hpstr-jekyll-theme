---
layout: post
title: "Git na apache2 przez davfs"
date: 2014-05-14 16:47:59 +0200
comments: true
categories: linux, git
---

Szybkie repozytorium GIT przez HTTP w Debianie

Tworzymy podkatalog w katalogu VHosta

``` bash
cd /var/www/domain.com
mkdir myrepo.git
```

Inicjacja repozytorium

``` bash
cd myrepo.git
git --bare init
```

Ustawienie praw dostępu

``` bash
chown -R www-data:www-data .
```

Dostosowanie gita pod http

``` bash
git update-server-info
```

Włączenie davfs
``` bash
a2enmod dav_fs
```

Dodanie konfiguracji davfs w `/etc/apache2/sites-enabled/domain.com`, najprostsza wersja bez autoryzacji:

``` xml
<Location /myrepo.git>
    DAV on           
    AuthType None    
</Location>            
```

lub trochę bardziej bezpieczna:

``` bash
htpasswd /etc/apache2/passwords/passwd_git username 
```

``` xml
<Location /myrepo.git>
      DAV on
      AuthType Basic
      AuthName "Git"
      AuthUserFile /etc/apache2/passwords/passwd_git
      Require valid-user
</Location>
```


Restart apache
``` bash
apache2 -k restart
```

Pierwszy test przez przeglądarkę: `http://domain.com/myrepo.git`