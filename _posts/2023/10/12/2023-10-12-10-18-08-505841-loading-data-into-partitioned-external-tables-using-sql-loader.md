---
layout: post
title: "Loading data into partitioned external tables using SQL Loader."
description: " "
date: 2023-10-12
tags: [loading, conclusion]
comments: true
share: true
---

In this blog post, we will explore how to load data into partitioned external tables using SQL Loader. Partitioning tables can greatly improve query performance and manageability, especially when dealing with large datasets. SQL Loader is a powerful tool that allows you to efficiently load data into Oracle databases.

## Table of Contents
- [What is partitioning?](#what-is-partitioning)
- [Creating partitioned external tables](#creating-partitioned-external-tables)
- [Loading data into partitioned external tables using SQL Loader](#loading-data-into-partitioned-external-tables-using-sql-loader)
- [Conclusion](#conclusion)

## What is partitioning? {#what-is-partitioning}
Partitioning is a technique used to divide a large database table into smaller, more manageable pieces called partitions. Each partition contains a subset of the data based on a defined partitioning key, such as a date or a range. Partitioning can greatly improve performance by allowing queries to only access relevant partitions, reducing the amount of data that needs to be scanned.

## Creating partitioned external tables {#creating-partitioned-external-tables}
Before we can load data into partitioned external tables using SQL Loader, we need to create the tables and define the partitioning scheme. Here is an example of creating a partitioned external table in Oracle:

```
CREATE TABLE sales
(
    sale_id     NUMBER,
    sale_date   DATE,
    sale_amount NUMBER
)
PARTITION BY RANGE (sale_date)
(
    PARTITION p2019 VALUES LESS THAN (TO_DATE('01-JAN-2020', 'DD-MON-YYYY')),
    PARTITION p2020 VALUES LESS THAN (TO_DATE('01-JAN-2021', 'DD-MON-YYYY')),
    PARTITION p2021 VALUES LESS THAN (TO_DATE('01-JAN-2022', 'DD-MON-YYYY'))
)
ORGANIZATION EXTERNAL (
    TYPE ORACLE_LOADER
    DEFAULT DIRECTORY sales_dir
    ACCESS PARAMETERS (
        RECORDS DELIMITED BY NEWLINE
        BADFILE 'sales.bad'
        LOGFILE 'sales.log'
        FIELDS TERMINATED BY ','
        (
            sale_id     INTEGER EXTERNAL,
            sale_date   CHAR(10) DATE MASK 'DD-MON-YYYY',
            sale_amount DECIMAL EXTERNAL
        )
    )
    LOCATION ('sales_data.txt')
);
```

In the above example, we create a partitioned table named "sales" with three partitions based on the "sale_date" column. Each partition is defined with a specific date range using the `VALUES LESS THAN` clause.

## Loading data into partitioned external tables using SQL Loader {#loading-data-into-partitioned-external-tables-using-sql-loader}
Once we have created partitioned external tables, we can use SQL Loader to load data into them. Here is an example of a control file that can be used with SQL Loader to load data into the partitioned "sales" table:

```
LOAD DATA
INFILE 'sales_data.txt'
INTO TABLE sales
APPEND
PRESERVE BLANKS
```

In the above example, we specify the data file to load (`sales_data.txt`) and the target table (`sales`). The `APPEND` directive tells SQL Loader to append the data to the existing table and the `PRESERVE BLANKS` option preserves leading and trailing blanks in the data.

To execute the SQL Loader command, use the following command in the terminal:

```
sqlldr username/password control=loader.ctl
```

Replace `username` and `password` with your database credentials and `loader.ctl` with the name of your control file.

## Conclusion {#conclusion}
Loading data into partitioned external tables using SQL Loader can be a powerful technique to efficiently load and manage large datasets in Oracle databases. Partitioning tables can improve query performance by selectively accessing relevant partitions. SQL Loader provides a convenient way to load data into these partitioned tables.

By following the steps outlined in this blog post, you can effectively load data into partitioned external tables using SQL Loader. Utilizing partitioning techniques and SQL Loader can significantly enhance the performance and manageability of your database systems.

#oracle #sqlloder