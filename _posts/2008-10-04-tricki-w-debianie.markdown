---
layout: post
title: "Tricki w Debianie"
date: 2008-10-04 08:54
comments: true
categories:
- Linux
---
Usuwanie ostatnio zainstalowanych (niepotrzebnie) pakietów:

```apt-get --purge remove `cat dpkg.log | grep " installed" | awk '{print $5}'` ```

Takie rzeczy w dystrybucjach debianopochodnych są po prostu cudowne
		