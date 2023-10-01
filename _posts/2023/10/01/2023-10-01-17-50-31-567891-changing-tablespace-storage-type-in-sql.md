---
layout: post
title: "Changing tablespace storage type in SQL"
description: " "
date: 2023-10-01
tags: [Oracle]
comments: true
share: true
---

In Oracle Database, a tablespace is used to store the physical data files for tables, indexes, and other database objects. Each tablespace has a storage type, which determines how the data is stored and managed.

Sometimes, it may be necessary to change the storage type of a tablespace to optimize performance or address disk space issues. This can be done in SQL using the `ALTER TABLESPACE` statement.

Here is an example of how to change the storage type of a tablespace in SQL:

```
ALTER TABLESPACE tablespace_name STORAGE(storage_parameters);
```

In the above statement, replace `tablespace_name` with the name of the tablespace you want to change, and `storage_parameters` with the parameters specific to the new storage type you want to use.

For example, if you want to change the tablespace named 'users' to use Automatic Segment Space Management (ASSM), you can use the following SQL statement:

```sql
ALTER TABLESPACE users STORAGE (SEGMENT SPACE MANAGEMENT AUTO);
```

This will change the storage type of the 'users' tablespace to use Automatic Segment Space Management.

Keep in mind that changing the storage type of a tablespace can have significant implications on performance and data management. Therefore, it is important to carefully evaluate the impact and perform thorough testing before making such changes in a production environment.

**#SQL #Oracle**

By using the above SQL statement, you can easily change the storage type of a tablespace in Oracle Database, allowing you to optimize performance and address disk space issues efficiently.