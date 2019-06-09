---
layout: default
title: MySQL
parent: Dashboard
nav_order: 2
---

# MySQL
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Primary key with JPA

With JPA specification you're allowed to define an strategy to create unique key values. Using @GeneratedValue, you choose between:
- AUTO ⇢ Hibernate selects the generation strategy based on the used dialect
- IDENTITY ⇢ Hibernate relies on an auto-incremented database column to generate the key
- SEQUENCE ⇢ Hibernate request the PK value from a database sequence
- TABLE ⇢ Hibernate uses a database table to simulate a sequence

Commonly, it's recommended using the SEQUENCE strategy because it allows Hibernate to use JDBC batching and other optimization strategies that require the delayed execution of SQL INSERT statements.

However, it requires a database sequence, and MySQL doesn’t support this feature. We use IDENTITY instead but taking in consideration that we're using an autoincrement and we won't use things like batch insert.
{: .fs-5 .ls-10 .code-example }

## Check and modify the AUTO_INCREMENT value
We can use this to set an specific value, restart it or even set an initial one.

```sql
SELECT AUTO_INCREMENT FROM information_schema.TABLES WHERE TABLE_SCHEMA = 'tableSchema' AND TABLE_NAME = 'tableName';
UPDATE information_schema.TABLES SET AUTO_INCREMENT= 27 WHERE TABLE_SCHEMA = 'tableSchema' AND TABLE_NAME = 'tableName';
```
