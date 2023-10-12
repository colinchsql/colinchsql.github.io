---
layout: post
title: "Setting up bad file and discard file in SQL Loader."
description: " "
date: 2023-10-12
tags: [database, SQLLoader]
comments: true
share: true
---

When loading data into an Oracle database using SQL Loader, it's important to have a mechanism in place to handle any data errors that may occur during the loading process. SQL Loader provides the option to divert error records into separate files, known as the bad file and discard file.

## What is a Bad File?
A bad file is a file that contains records that were rejected during the data loading process due to errors or inconsistencies. These errors can be related to data formatting, data type mismatches, or other constraints defined in the table.

To specify a bad file in SQL Loader, you can use the `BAD` parameter followed by the name of the file where the rejected records should be written. Here's an example of how to set up a bad file in SQL Loader:

```sql
sqlldr username/password control=loader.ctl log=loader.log bad=loader.bad
```
In the above example, `loader.bad` is the file where the rejected records will be written. You can choose any name for your bad file.

## What is a Discard File?
A discard file is a file that contains records that were successfully parsed and loaded into the table but discarded due to various reasons. These records may not meet the specific criteria or business rules defined for a particular dataset.

To specify a discard file in SQL Loader, you can use the `DISCARD` parameter followed by the name of the file where the discarded records should be written. Here's an example:

```sql
sqlldr username/password control=loader.ctl log=loader.log discard=loader.dsc
```

In the above example, `loader.dsc` is the file where the discarded records will be written. Again, you can choose any suitable name for your discard file.

## Conclusion
Setting up bad file and discard file in SQL Loader allows you to capture rejected and discarded records during the data loading process. These files help in troubleshooting data quality issues and provide insights into potential data sources or transformation problems. Remember to properly handle these files and analyze their contents to ensure data integrity and accuracy in your Oracle database.

_#database #SQLLoader_