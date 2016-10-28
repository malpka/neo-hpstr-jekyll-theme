---
layout: post
title: "1 liner - pobieranie wersji .NET framework dla bibliotek w katalogu"
date: 2012-10-08 10:41
comments: true
categories:
- C#
- Programowanie
- Techblog
---
<p>Przydatne, gdy trzeba określić ostateczną wersję frameworka, np do wymagań instalatora.</p>
<p></p>
<p><code>for %p in (*.dll) do @echo %p &amp;&amp; @ildasm.exe %p /metadata[=MDHEADER] /text /noil | grep -E -o "version: v[a-z0-9\.]+"</code></p>
<p>Nie ma grepa na Windowsie? Jak tak można w ogóle pracować... ;)</p>
<p><a href="http://gnuwin32.sourceforge.net/packages/grep.htm">http://gnuwin32.sourceforge.net/packages/grep.htm</a></p>
<p>Przykładowe wyjście:</p>
<p><code>Microsoft.Practices.CompositeUI.dll<br>
version: v2.0.50727<br>
Microsoft.Practices.CompositeUI.WinForms.dll<br>
version: v2.0.50727<br>
Microsoft.Practices.EnterpriseLibrary.Caching.dll<br>
version: v2.0.50727<br>
Microsoft.Practices.EnterpriseLibrary.Common.dll<br>
version: v2.0.50727</code></p>
<p></p>
<p><a href="http://stackoverflow.com/questions/3460982/determine-net-framework-version-for-dll">Źródło inspiracji</a></p>
<p>Oczywiście są również wersje okienkowe, jak wspomniany w odpowiedziach <a href="http://www.jetbrains.com/decompiler/">dotPeek</a>.</p>
		