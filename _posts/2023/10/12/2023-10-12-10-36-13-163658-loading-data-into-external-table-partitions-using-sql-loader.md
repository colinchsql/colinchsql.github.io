---
layout: post
title: "Loading data into external table partitions using SQL Loader."
description: " "
date: 2023-10-12
tags: [Oracle]
comments: true
share: true
---

In this blog post, we will explore how to load data into external table partitions using SQL Loader. Partitioning tables is a common practice in databases to improve performance and manage data efficiently. External tables allow us to access data stored outside the database as if it were a regular table. SQL Loader is a powerful tool for loading data into Oracle databases, and it supports loading data into partitioned tables by specifying the partition key values.

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Creating the External Table](#creating-the-external-table)
4. [Creating the Partitioned Table](#creating-the-partitioned-table)
5. [Loading Data into Partitions](#loading-data-into-partitions)
6. [Conclusion](#conclusion)

## Introduction

Partitioning tables can significantly improve query performance, especially in scenarios where large volumes of data need to be processed efficiently. Using external tables, we can seamlessly load data from external sources, such as flat files, into partitioned tables in Oracle databases. SQL Loader is a widely used utility that can efficiently load data into partitioned tables.

## Prerequisites

Before we begin, make sure you have the following prerequisites:

- Oracle Database installed and running
- Access to the SQL Loader utility
- Basic understanding of SQL and Oracle Database concepts

## Creating the External Table

To load data into external table partitions, we first need to create the external table. An external table is a definition that provides access to data stored outside the database.

```sql
CREATE TABLE ext_data (
  id NUMBER,
  name VARCHAR2(100),
  date_of_birth DATE
)
ORGANIZATION EXTERNAL (
  TYPE ORACLE_LOADER
  DEFAULT DIRECTORY ext_dir
  ACCESS PARAMETERS (
    RECORDS DELIMITED BY NEWLINE
    FIELDS TERMINATED BY ','
    MISSING FIELD VALUES ARE NULL
  )
  LOCATION ('data.csv')
)
REJECT LIMIT UNLIMITED;
```

In the above example, we are creating an external table `ext_data` with columns `id`, `name`, and `date_of_birth`. The external table is defined to use the Oracle Loader access driver and is associated with a directory `ext_dir` that points to the location of the data file `data.csv`.

## Creating the Partitioned Table

Next, we need to create the partitioned table where the data will be loaded.

```sql
CREATE TABLE partitioned_data (
  id NUMBER,
  name VARCHAR2(100),
  date_of_birth DATE
)
PARTITION BY RANGE (date_of_birth)
INTERVAL (NUMTODSINTERVAL(1, 'DAY'))
(
  PARTITION p_default VALUES LESS THAN (TO_DATE('01-JAN-2022', 'DD-MON-YYYY'))
);
```

In this example, we are creating a partitioned table `partitioned_data` with columns `id`, `name`, and `date_of_birth`. The table is partitioned using the `date_of_birth` column, with one partition defined as `p_default` that covers all values less than `01-JAN-2022`.

## Loading Data into Partitions

To load data into the partitioned table using SQL Loader, we need to specify the `PARTITION` keyword followed by the partition name and the appropriate partition key values in the control file (`.ctl`).

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE partitioned_data PARTITION (p_default)
APPEND
FIELDS TERMINATED BY ','
TRAILING NULLCOLS
(
  id,
  name,
  date_of_birth "YYYYMMDD"
)
```

In the above control file snippet, we are instructing SQL Loader to load data from `data.csv` into the `partitioned_data` table, specifically the `p_default` partition. The `APPEND` keyword appends the loaded data to the existing data in the partitioned table.

## Conclusion

In this blog post, we learned how to load data into external table partitions using SQL Loader. Partitioning tables can greatly improve query performance and manage large volumes of data efficiently. SQL Loader provides a convenient way to load data into partitioned tables by specifying the partition key values. By using external tables, we can seamlessly load data from external sources into partitioned tables in Oracle databases.

---

**#SQL** **#Oracle**