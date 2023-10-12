---
layout: post
title: "Loading data with nested tables using SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

In this blog post, we will explore how to load data with nested tables using SQL Loader. Nested tables are a powerful feature in Oracle databases that allow you to store and manage complex data structures within a single column. By utilizing SQL Loader, we can efficiently load data into these nested tables. Let's dive into the steps involved.

## Table of Contents
- [What are Nested Tables?](#what-are-nested-tables)
- [SQL Loader](#sql-loader)
- [Loading Data into Nested Tables](#loading-data-into-nested-tables)
- [Conclusion](#conclusion)

## What are Nested Tables?

Nested tables are Oracle database objects that can hold an array of elements within a single column. They provide a way to store and manipulate collections of data. Each element within a nested table can be of any compatible datatype, allowing you to create complex data structures. Nested tables provide the flexibility to store and query hierarchical data efficiently.

## SQL Loader

SQL Loader is a powerful tool provided by Oracle to load data into the database from external files. It supports various file formats, such as CSV, fixed-width, and XML. SQL Loader utilizes control files to define the data format and loading rules.

To load data into nested tables using SQL Loader, we need to define the appropriate control file to handle the complex structure and relationships.

## Loading Data into Nested Tables

To load data into nested tables using SQL Loader, follow these steps:

1. **Create the Nested Table:** First, create the nested table in your Oracle database. Specify the datatypes of the elements within the nested table.
```sql
CREATE TYPE employee_type AS OBJECT (
    employee_id NUMBER,
    employee_name VARCHAR2(50),
    ...
);

CREATE TYPE employee_list AS TABLE OF employee_type;
```

2. **Create the External Table:** Next, create an external table that corresponds to your nested table. It acts as an interface between the external file and the nested table.
```sql
CREATE TABLE employee_loader (
    employee_data employee_list
)
ORGANIZATION EXTERNAL (
    TYPE ORACLE_LOADER
    DEFAULT DIRECTORY data_dir
    ACCESS PARAMETERS (
        RECORDS DELIMITED BY NEWLINE
        FIELDS TERMINATED BY ','
        (employee_id, employee_name, ...)
    )
    LOCATION ('employees.csv')
);
```

3. **Create the Control File:** Create a control file that defines the structure and relationships between the external table and the nested table. Specify the appropriate fields and loading rules.
```plaintext
LOAD DATA
INFILE 'employees.csv'
APPEND INTO TABLE employee_loader
FIELDS TERMINATED BY ","
(
  employee_data TYPE employee_list
    (     
      employee_id CHAR(100),
      employee_name CHAR(100),
      ...
    )
)
```

4. **Execute SQL Loader:** Run SQL Loader with the control file to load the data into the nested table.
```bash
sqlldr control=control_file.ctl
```

5. **Verify the Data:** Once the loading process is complete, verify the data has been successfully loaded into the nested table.
```sql
SELECT * FROM employee_loader;
```

## Conclusion

Loading data into nested tables using SQL Loader is an efficient and convenient way to handle complex data structures within an Oracle database. By following the steps outlined in this blog post, you can easily load data into nested tables and leverage the power of Oracle's nested table feature.

To learn more about SQL Loader and nested tables, refer to the Oracle documentation and explore further examples and use cases.