---
layout: post
title: "Extract data from ovh domain list with xpath"
date: 2016-03-22 14:17:00 +0200
comments: true
categories: bash, linux
---


```
//a[starts-with(@title, "Twoja domena")]/../../td[@data-title='Rozszerzenia']/a/text()[1]
//a[starts-with(@title, "Twoja domena")]/../../td[@data-title='Odnowienie']/span[last()]/text()[1]
```

