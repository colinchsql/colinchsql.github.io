---
layout: post
title: "Using SQL Loader with external tables."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

In Oracle, SQL Loader is a powerful tool for loading data from external files into Oracle tables. It provides a fast and efficient way to load large datasets into the database. However, when dealing with very large datasets, using SQL Loader with external tables can offer even better performance.

## What are External Tables?
External tables are read-only tables that map to data in external files. They are defined and controlled by the database but the actual data resides in files outside the database. External tables provide a way to access external data without the need to load it into a regular Oracle table.

## Benefits of Using External Tables with SQL Loader
When using SQL Loader with external tables, you can take advantage of several benefits:

- **Performance**: External tables can be significantly faster than loading data into regular tables because the data is accessed directly from the files, without the overhead of inserting rows.
- **Parallel Processing**: With external tables, you can use parallel processing to load data into multiple tables simultaneously, further improving performance.
- **Data Manipulation**: External tables allow you to perform SQL operations on the external data, such as filtering, joining, and aggregating, as if it were regular data in the database.

## Steps to Use SQL Loader with External Tables

To use SQL Loader with external tables, follow these steps:

1. **Create the External Table Definition**: Create an external table definition that specifies the structure of the data in the external file. This is similar to creating a regular table, but you use the `ORGANIZATION EXTERNAL` clause to indicate that it is an external table.

```sql
CREATE TABLE external_data 
(
  id   NUMBER,
  name VARCHAR2(100)
)
ORGANIZATION EXTERNAL
(
  TYPE ORACLE_LOADER
  DEFAULT DIRECTORY data_dir
  ACCESS PARAMETERS
  (
    RECORDS DELIMITED BY NEWLINE
    BADFILE 'external_data.bad'
    LOGFILE 'external_data.log'
    SKIP 1
    FIELDS TERMINATED BY ','
    (
      id,
      name
    )
  )
  LOCATION ('data.csv')
)
REJECT LIMIT UNLIMITED;
```

2. **Load Data using SQL Loader**: Use the `sqlldr` command-line utility to load data into the external table. Specify the control file that defines how the data should be loaded.

```shell
sqlldr username/password@service CONTROL=load_data.ctl
```

The control file (load_data.ctl) should contain the necessary instructions for SQL Loader to load data correctly.

3. **Access the External Table**: Once the data has been loaded, you can query and manipulate it like any other table in the database.

```sql
SELECT * FROM external_data;
```

## Conclusion
Using SQL Loader with external tables is a powerful way to load and access large datasets in Oracle. It offers better performance and flexibility compared to loading data into regular tables. By following the steps outlined above, you can take advantage of this feature and efficiently load data from external files into your Oracle database.