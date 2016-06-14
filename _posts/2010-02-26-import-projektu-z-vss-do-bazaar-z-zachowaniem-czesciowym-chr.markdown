---
layout: post
title: "Import projektu z VSS do Bazaar z zachowaniem (częściowym) chronologii zmian"
date: 2010-02-26 09:23
comments: true
categories:
- Ogólne
---
<p>Importing project from Microsoft Visual Sourcesafe (VSS) to Bazaar SCM with partial version preservation for dummies.</p>
<p>Code snippet for january :)</p>
<p></p>
<p></p>
<pre>
@echo Off<br><br>set SSDIR=Y:\<br>set SSUSER=username<br>set SSPWD=<br><br>bzr init<br><br>FOR /L %%d in (1, 1, 31) do (<br>"C:\Program Files\Microsoft Visual SourceSafe\ss.exe" get $/Project -R -GTU -Vd2010/1/%%d<br>bzr add<br>bzr del<br>bzr ci -m "2010/1/%%d"<br>pause<br>)<br>
</pre>
<p>
<p></p>
		