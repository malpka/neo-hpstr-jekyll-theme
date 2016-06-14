---
layout: post
title: "Pyhon - hurtowa zmiana atrybutów w xml"
date: 2011-01-03 12:33
comments: true
categories:
- Do zapamiętania
- Python
---
<p>Kolejne kilka linijek, które ułatwią mi kiedyś życie.</p>
<p>Czasem zdarza się, że pobieranie wersji pliku dll w C# zwraca śmieci zamiast standardowych A.B.C.D. W moim przypadku biblioteki stworzone chyba w delphi miały zwyczaj stosować przecinki zamiast kropek, albo dodawać spacje między liczbami.</p>
<p>Ponieważ korzystam z narzędzia, które generuje mi do xmla listę plików w katalogu, z uwzględnieniem sumy kontrolnej i wersji, a nie miałem jego źródeł, trzeba było napisać szybką łatkę na wygenerowane dane.</p>
<p></p>
<pre>
from xml.dom import minidom
DOMTree = minidom.parse('filelist.xml')
cNodes = DOMTree.childNodes
for i in cNodes[0].getElementsByTagName("File"):
        version = i.getAttribute("version")
        version = version.replace(",", ".")
        version = version.replace(" ", "")
        i.setAttribute("version", version)

f = open('filelist.xml', 'w')
DOMTree.writexml(f)
f.close()
</pre>
<p></p>
		