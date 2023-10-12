---
layout: post
title: "Loading data with composite primary keys using SQL Loader."
description: " "
date: 2023-10-12
tags: [SQLLoader, CompositePrimaryKeys]
comments: true
share: true
---

When working with databases, it is common to have tables with composite primary keys, which consist of multiple columns. Loading data into such tables can be a bit trickier than loading into tables with a single primary key column. In this blog post, we will explore how to load data with composite primary keys using SQL Loader.

## 1. Understanding Composite Primary Keys

A composite primary key is a combination of two or more columns that uniquely identifies each row in a table. For example, let's consider a table named `employees` with columns `employee_id` and `department_id` as the composite primary key.

```sql
CREATE TABLE employees (
    employee_id NUMBER,
    department_id NUMBER,
    employee_name VARCHAR2(100),
    -- other columns
    CONSTRAINT pk_employees PRIMARY KEY (employee_id, department_id)
);
```

## 2. Creating Control File

To load data into a table with a composite primary key using SQL Loader, we need to create a control file. The control file specifies the format of the data file and maps the columns in the data file to the columns in the table.

```sql
LOAD DATA
INFILE 'data.csv'
APPEND INTO TABLE employees
FIELDS TERMINATED BY ',' 
(
    employee_id,
    department_id,
    employee_name
)
```
Make sure to adjust the `FIELDS TERMINATED BY` clause according to the delimiter used in your data file.

## 3. Preparing the Data File

The next step is to prepare the data file that contains the data to be loaded into the table. The data file should have the same format as specified in the control file.

Example of `data.csv`:
```csv
123,1,John Doe
456,2,Jane Smith
789,3,Michael Johnson
```

## 4. Running SQL Loader

Once you have the control file and the data file ready, you can load the data using SQL Loader. Open a command prompt or terminal and run the following command:

```
sqlldr username/password control=control.ctl log=log.log
```

Replace `username` and `password` with your database credentials, `control.ctl` with the name of your control file, and `log.log` with the desired name for the log file.

## Conclusion

Loading data with composite primary keys using SQL Loader requires creating a control file that specifies the format of the data file and mapping the columns correctly. By following the steps outlined in this blog post, you should be able to successfully load data into tables with composite primary keys.

#hashtags: #SQLLoader #CompositePrimaryKeys