---
layout: post
title: "Loading data into tables with virtual columns using SQL Loader."
description: " "
date: 2023-10-12
tags: [oracle, sqlloader]
comments: true
share: true
---

Virtual columns are a powerful feature in Oracle database that allows you to define a column in a table that does not store any data physically, but gets computed dynamically based on the expressions you define. This feature is useful when you want to have a calculated column in your table without the need to store the data redundantly.

In this blog post, we will explore how to load data into tables with virtual columns using SQL Loader, a powerful tool for data loading in Oracle databases.

## Table structure

Let's start by creating a simple table with a virtual column:

```sql
CREATE TABLE employees (
    id NUMBER,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    full_name VARCHAR2(100) GENERATED ALWAYS AS (first_name || ' ' || last_name) VIRTUAL
);
```

Here, we have a table called `employees` with columns `id`, `first_name`, `last_name`, and `full_name`, which is a virtual column that concatenates the `first_name` and `last_name` columns.

## Creating the control file

Next, we need to create a control file for SQL Loader, which specifies how the data should be loaded into the table. Below is an example of a control file (`employees.ctl`) for loading data into the `employees` table:

```plain
LOAD DATA
INFILE 'employees.csv'
INTO TABLE employees
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
TRAILING NULLCOLS
(
    id,
    first_name,
    last_name
)
```

In this control file, we specify the data file (`employees.csv`) as the input file, and define the fields and their corresponding columns that need to be loaded into the `employees` table.

## Loading data using SQL Loader

To load the data into the table using SQL Loader, you need to execute the following command:

```shell
sqlldr username/password@database control=employees.ctl log=employees.log
```

Make sure to replace `username/password@database` with the appropriate values for your Oracle database. The `control` parameter specifies the control file we created earlier, and the `log` parameter specifies the log file where the load results will be written.

Once the SQL Loader finishes, you can query the `employees` table to verify that the data has been loaded successfully, including the virtual column:

```sql
SELECT * FROM employees;
```

## Conclusion

In this blog post, we learned how to load data into tables with virtual columns using SQL Loader. Virtual columns in Oracle database provide a flexible and efficient way to define computed columns without the need to store redundant data. By using SQL Loader, we can easily load data into tables with virtual columns and take advantage of the powerful features offered by the Oracle database.

#oracle #sqlloader