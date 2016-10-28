---
layout: post
title: "Own mailserver - Debian 7 Wheezy VPS - Part 3 - database"
date: 2014-07-15 07:47:59 +0200
comments: true
categories: vps, linux
---

Let's map the virtual-* postfix configuration into mysql database

## Create database

``` bash
mysqladmin -p create mailserver
``` 

Enter mysql root password

``` bash
mysql -p mailserver
```

``` sql
GRANT SELECT ON mailserver.*
TO 'mailuser'@'127.0.0.1'
IDENTIFIED BY 'passw0rd';

CREATE TABLE `virtual_domains` (
  `id` int(11) NOT NULL auto_increment,
  `name` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `virtual_users` (
  `id` int(11) NOT NULL auto_increment,
  `domain_id` int(11) NOT NULL,
  `password` varchar(32) NOT NULL,
  `email` varchar(100) NOT NULL,
  `path` varchar(100) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`),
  FOREIGN KEY (domain_id) REFERENCES virtual_domains(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `virtual_aliases` (
  `id` int(11) NOT NULL auto_increment,
  `domain_id` int(11) NOT NULL,
  `source` varchar(100) NOT NULL,
  `destination` varchar(100) NOT NULL,
  PRIMARY KEY (`id`),
  FOREIGN KEY (domain_id) REFERENCES virtual_domains(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


``` sql
INSERT INTO `mailserver`.`virtual_domains` (
  `id` ,
  `name`
)
VALUES (
  '1', 'test.codemonkey.pl'
);

INSERT INTO `mailserver`.`virtual_users` (
  `id` ,
  `domain_id` ,
  `password` ,
  `email` ,
  `path` 
)
VALUES (
  '1', '1', MD5( 'paSs' ) , 'malpka@test.codemonkey.pl', 'test.codemonkey.pl/malpka'
);

INSERT INTO `mailserver`.`virtual_aliases` (
  `id`,
  `domain_id`,
  `source`,
  `destination`
)
VALUES (
  '1', '1', 'malpka2@test.codemonkey.pl', 'malpka@test.codemonkey.pl'
);

```

## Reconfigure postfix

### Enable mysql configuration

``` bash
apt-get install postfix-mysql
```

## Configure mysql for virtual_mailbox_domains

``` bash
cat << EOF > /etc/postfix/virtual_mailbox_domains_mysql
user = mailuser
password = passw0rd
hosts = 127.0.0.1
dbname = mailserver
query = SELECT 1 FROM virtual_domains WHERE name='%s'
EOF

postconf -e virtual_mailbox_domains=mysql:/etc/postfix/virtual_mailbox_domains_mysql
postmap /etc/postfix/virtual_mailbox_domains_mysql
```

## Configure mysql for virtual_mailbox_maps

``` bash
cat << EOF > /etc/postfix/virtual_mailbox_maps_mysql
user = mailuser
password = passw0rd
hosts = 127.0.0.1
dbname = mailserver
query = SELECT path FROM virtual_users WHERE email='%s'
EOF

postconf -e virtual_mailbox_maps=mysql:/etc/postfix/virtual_mailbox_maps_mysql
postmap /etc/postfix/virtual_mailbox_maps_mysql
```

Default MBox file for the virtual mail is a concatenation of `virtual_mailbox_base` and the result of above query, so for our example it will be `/var/vmail/test.codemonkey.pl/malpka`.


## Configure mysql for virtual_alias_maps

``` bash
cat << EOF > /etc/postfix/virtual_alias_maps_mysql
user = mailuser
password = passw0rd
hosts = 127.0.0.1
dbname = mailserver
query = SELECT destination FROM virtual_aliases WHERE source='%s'
EOF

postconf -e virtual_alias_maps=mysql:/etc/postfix/virtual_alias_maps_mysql
postmap /etc/postfix/virtual_alias_maps_mysql
```

## Final configuration

``` bash
chgrp postfix /etc/postfix/virtual*mysql
chmod u=rw,g=r,o= /etc/postfix/virtual*mysql

postfix reload
```