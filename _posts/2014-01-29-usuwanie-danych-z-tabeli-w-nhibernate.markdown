---
layout: post
title: "Usuwanie danych z tabeli w nHibernate"
date: 2014-01-29 10:00:49 +0100
comments: true
categories: 
---
Najbardziej generalny sposób, na jaki trafiłem.

``` c#
private static void CleanUpTable<T>(ISessionFactory sessionFactory)
{
    var metadata = sessionFactory.GetClassMetadata(typeof(T)) as NHibernate.Persister.Entity.AbstractEntityPersister;
    string table = metadata.TableName;

    using (ISession session = sessionFactory.OpenSession())
    {
        using (var transaction = session.BeginTransaction())
        {
            string deleteAll = string.Format("DELETE FROM \"{0}\"", table);
            session.CreateSQLQuery(deleteAll).ExecuteUpdate();

            transaction.Commit();
        }
    }
}
```
Sposób użycia:
``` c#
CleanUpTable<Person>(sessionFactory);
```
[Źródło](http://stackoverflow.com/a/16861155/1434646)
