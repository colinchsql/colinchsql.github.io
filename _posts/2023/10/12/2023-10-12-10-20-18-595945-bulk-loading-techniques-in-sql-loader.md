---
layout: post
title: "Bulk loading techniques in SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

SQL Loader is a powerful tool used to load data into Oracle Database from external files. It supports various bulk loading techniques that can significantly improve the performance of data loading. In this blog post, we will explore some of these techniques and discuss their advantages.

## Table of Contents
- [Direct Path Load](#direct-path-load)
- [Conventional Path Load](#conventional-path-load)
- [Parallel Load](#parallel-load)
- [External Tables](#external-tables)
- [Conclusion](#conclusion)
- [References](#references)

## Direct Path Load

The direct path load is the fastest loading technique provided by SQL Loader. It bypasses much of the Oracle Database processing and writes data directly into database blocks, bypassing the buffer cache. This technique is ideal for large datasets, as it minimizes overhead and maximizes performance.

To perform a direct path load, you can use the `DIRECT=true` parameter in your control file or specify `DIRECT=TRUE` in the command line. Additionally, you can optimize the load by disabling constraints and indexes using the `INDEXES=DISABLED` parameter. Once the data is loaded, you can enable the constraints and indexes.

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
APPEND
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
( 
  emp_id,
  emp_name,
  emp_salary
)
DIRECT=true
INDEXES=DISABLED
```

## Conventional Path Load

The conventional path load is the default loading technique used by SQL Loader. It performs data loading by inserting each row into the database through conventional SQL statements. This method is slower compared to direct path load but it supports more features such as complex transformations and validations.

Conventional path load is suitable for smaller datasets or when data transformations are required during the loading process. It loads data using the server's buffer cache, which can be beneficial if the data needs to be manipulated before being inserted into the database.

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
APPEND
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
( 
  emp_id,
  emp_name,
  emp_salary
)
```

## Parallel Load

If you have a large dataset and want to further improve the loading performance, you can use the parallel load technique. SQL Loader supports parallel data loading, allowing multiple threads to load data simultaneously into separate partitions or segments of a table.

To enable parallel load, you can specify the `PARALLEL=true` parameter in the control file or the command line. The degree of parallelism can be adjusted using the `PARALLEL_THREADS_PER_CPU` parameter, which determines the number of parallel threads per CPU.

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
APPEND
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
( 
  emp_id,
  emp_name,
  emp_salary
)
PARALLEL=true
PARALLEL_THREADS_PER_CPU=2
```

## External Tables

In addition to SQL Loader, Oracle Database also provides the concept of External Tables, which allows you to access external data files as if they were database tables. External Tables provide a convenient way to load data into the database without the need for a separate data loading tool.

By defining the structure of the external file and specifying the access method, Oracle Database can transparently access and query the data. External Tables support all the querying capabilities of regular database tables, making them a versatile method for loading and querying data.

```sql
CREATE TABLE employees_ext (
  emp_id NUMBER,
  emp_name VARCHAR2(100),
  emp_salary NUMBER
)
ORGANIZATION EXTERNAL (
  TYPE ORACLE_LOADER
  DEFAULT DIRECTORY data_dir
  ACCESS PARAMETERS (
    RECORDS DELIMITED BY NEWLINE
    FIELDS TERMINATED BY ','
    OPTIONALLY ENCLOSED BY '"'
    MISSING FIELD VALUES ARE NULL
  )
  LOCATION ('data.csv')
)
REJECT LIMIT UNLIMITED;
```

## Conclusion

SQL Loader provides several bulk loading techniques that can greatly improve the performance of data loading into Oracle Database. Whether you need the fastest loading approach or require more flexibility for data transformations, SQL Loader has you covered. Additionally, the concept of External Tables provides an alternative way to access and load external data files.

By understanding these techniques and choosing the appropriate method based on your requirements, you can efficiently load large volumes of data and optimize the data loading process.

## References

- [Oracle Database SQL Loader Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/21/sutil/oracle-sql-loader.html)
- [Oracle External Tables Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/21/nlspg/external-tables.html)