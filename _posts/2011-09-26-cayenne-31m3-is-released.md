---
layout: post
title:  Cayenne 3.1M3 is Released
date:   2011-9-26
---

We are glad to announce 3.1M3 release of Cayenne. This is an important milestone on our way to Beta. In fact there is a good chance that the next release will be announced as Beta. Upgrade to M3 is strongly recommended to all 3.1 users, as it contains some critical bug fixes. The highlights of the M3:

* Core API improvements - cleaner vararg APIs in ObjectContext and Cayenne classes, ObjectContext.localObject(Object), etc.
* Switching more of the internals to DI (query cache providers, loggers, various strategies controlling ObjectContext behavior, etc.). We'll keep working on this, so M4 will have more of it, and in fact there are a number of existing patches waiting for review (e.g. DI-based ExtendedTypes).
* New QueryCache implementation based on EHCache (not thoroughly tested yet, so user feedback will be very helpful).
* Refactoring of "cayenne-lifecycle" based on experience using it in the real apps.
* Fixing a number of critical bugs.

[Download link](/download.html)

And now the full release notes:

## Changes/New Features

* CAY-943 Support multiple cayenne.xml files in the project
* CAY-1266 Joint prefetches with fetch limit and offset do not work on Oracle
* CAY-1461 CayenneModeler: remove ScopeMVC dependency - ObjRelationshipInfoDialog
* CAY-1556 Add path construction feature to make constructing paths from constants easier for queries and orderings
* CAY-1525 CharType: don't trim spaces on the left
* CAY-1537 Implement ObjectContext local caches as NestedQueryCache over the shared cache
* CAY-1544 Remove jdk1.6 module from Cayenne sources
* CAY-1545 cayenne-lifecycle Referenceable handler refactoring
* CAY-1547 cayenne-lifecycle: support for setting UuidRelationships
* CAY-1549 Migrate BatchQueryBuilderFactory to DI
* CAY-1553 cayenne-lifecycle: @SortWeight annotation
* CAY-1573 QueryLogger to DI JdbcEventLogger migration
* CAY-1584 Improve Cayenne modeler re-ordering named query in the cayenne map xml
* CAY-1586 New extension point: a strategy for retaining objects in the ObjectStore
* CAY-1590 DDL generation without a live datasource
* CAY-1594 DI extension point: turning on/off cross-ObjectContext synchronization
* CAY-1595 EHCache implementation of Provider<QueryCache>
* CAY-1598 Per DataMap listeners are called for all entities in DataDomain
* CAY-1599 Annotation-based global listeners registration
* CAY-1605 Switch Cayenne to use unified Maven repository
* CAY-1606 Change CayenneModeler new object naming strategy
* CAY-1610 ObjectContext API to use varargs
* CAY-1611 ObjectContext API improvement - better 'localObect' method

## Bug Fixes

* CAY-1469 Modeler: dbRelationships renaming problem
* CAY-1526 Preferences: java.lang.IllegalArgumentException: Key too long
* CAY-1539 Incorrect offset handling on some queries against database with supported LIMIT/OFFSET clauses
* CAY-1546 cayenne-lifecycle: UuidBatchFault concurrency issues
* CAY-1555 Unpublished dependencies of Maven plugins
* CAY-1575 Error generating Embeddable classes in Cayenne Modeler
* CAY-1577 SQL queries for LIKE expressions with escape character generated with syntax errors
* CAY-1581 Not-Escaping <> during serialization to *.map.xml
* CAY-1583 context.getObjectStore() returning null causing NullpointerException in DataMergeHandler
* CAY-1585 SelectQuery automatic cache key needs FetchOffset
* CAY-1591 CayenneModeler: keyboard shortcuts causing havoc in SQLTemplate SQL editor
* CAY-1596 setFetchOffset & setFetchLimit issue under SQL Server 2008 R2 64Bit
* CAY-1602 OSCache clustering should be shared per JVM - @CacheGroup annotation causes creation of too many cluster listeners