---
layout: post
title: "Tworzenie schematu XSD z XML"
date: 2014-01-06 15:13:53 +0100
comments: true
categories: 
---

Przy okazji [migracji danych z Joggera na Octopress](/2014/01/05/migracja-jogger-octopress/)
potrzebowałem szybko dostać schemat struktury całego XML'a eksportu, aby się upewnić, czy w
XML'u nie czekają na mnie żadne niespodzianki.
Są dostępne różne narzędzia, łącznie z tymi [online](http://www.freeformatter.com/xsd-generator.html),
ale okazało się że szybko da się to wykonać z wykorzystaniem klasy
[XmlSchemaInference](http://msdn.microsoft.com/en-us/library/system.xml.schema.xmlschemainference.aspx) z .NET:

``` c# Pobieranie XSD z XML w C#
XmlReader reader = XmlReader.Create("jogger_eksport.xml");
XmlSchemaSet schemaSet = new XmlSchemaSet();
XmlSchemaInference schema = new XmlSchemaInference();

schemaSet = schema.InferSchema(reader);

using (TextWriter writer = File.CreateText("jogger_eksport.xsd"))
  foreach (XmlSchema s in schemaSet.Schemas())
    s.Write(writer);
```

otrzymałem XSD, oczywiście bardzo ogólny, joggerowego eksportu:

``` xml
<?xml version="1.0" encoding="windows-1250"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="jogger">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="user">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="jid" type="xs:string" />
              <xs:element name="domain" type="xs:string" />
              <xs:element name="alias" />
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element maxOccurs="unbounded" name="entry">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="date" type="xs:string" />
              <xs:element name="jid" type="xs:string" />
              <xs:element name="level_id" type="xs:unsignedByte" />
              <xs:element name="comment_mode" type="xs:unsignedByte" />
              <xs:element name="subject" type="xs:string" />
              <xs:element name="body" type="xs:string" />
              <xs:element name="tags" type="xs:string" />
              <xs:element name="permalink" type="xs:string" />
              <xs:element name="trackback" type="xs:string" />
              <xs:element maxOccurs="unbounded" name="category" type="xs:string" />
              <xs:element minOccurs="0" maxOccurs="unbounded" name="comment">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element name="date" type="xs:string" />
                    <xs:element name="nick" type="xs:string" />
                    <xs:element name="nick_url" type="xs:string" />
                    <xs:element name="body" type="xs:string" />
                    <xs:element name="ip" type="xs:string" />
                    <xs:element name="trackback" />
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```
