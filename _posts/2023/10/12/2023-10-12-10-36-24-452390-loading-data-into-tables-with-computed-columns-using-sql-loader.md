---
layout: post
title: "Loading data into tables with computed columns using SQL Loader."
description: " "
date: 2023-10-12
tags: [oracle, SQLLoader]
comments: true
share: true
---

When using SQL Loader to load data into tables, you may come across situations where you need to populate computed columns. Computed columns are columns whose values are derived from expressions or functions based on other columns in the same row. In this blog post, we will explore how to load data into tables with computed columns using SQL Loader.

## Table Structure

Let's start by creating a sample table with a computed column:
```sql
CREATE TABLE employees (
  id INT,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  salary INT,
  bonus_percentage DECIMAL(5,2),
  total_bonus AS (salary * bonus_percentage),
  total_salary AS (salary + total_bonus)
);
```

In the above example, the `total_bonus` column is computed by multiplying the `salary` column with the `bonus_percentage` column, and the `total_salary` column is computed by adding the `salary` column with the `total_bonus` column.

## SQL Loader Control File

To load data into the table, we need to provide a control file to SQL Loader. The control file specifies the file format, the table structure, and how to handle the data.

Here is an example of a control file (`employees.ctl`) that loads data into the `employees` table:
```sql
OPTIONS (SKIP=1)
LOAD DATA
INFILE 'employees.dat'
BADFILE 'employees.bad'
DISCARDFILE 'employees.dsc'
INSERT
INTO TABLE employees
FIELDS TERMINATED BY ','
TRAILING NULLCOLS
(
  id,
  first_name,
  last_name,
  salary,
  bonus_percentage
)
```

In the above control file, we specify the input file name using `INFILE`. The `FIELDS TERMINATED BY ','` statement indicates that the fields in the data file are separated by commas. We also specify the column mapping between the data file and the table columns.

## Data File

Now, let's create a sample data file (`employees.dat`) to load into the table:
```csv
1,John,Doe,5000,0.1
2,Jane,Smith,7000,0.15
3,Michael,Johnson,6000,0.12
```

In the above data file, each line represents a row of data, with columns separated by commas.

## Loading Data using SQL Loader

To load the data into the `employees` table using SQL Loader, you can execute the following command in the command line:
```
sqlldr username/password control=employees.ctl log=employees.log
```

Ensure to replace `username` and `password` with your database credentials.

After executing the command, SQL Loader will read the control file, locate the data file, and start loading data into the table. It will generate a log file (`employees.log`) that contains information about the loading process, such as the number of rows processed, any errors encountered, and more.

## Conclusion

In this blog post, we explored how to load data into tables with computed columns using SQL Loader. By creating a control file that specifies the input file format and column mapping, you can easily load data into tables with computed columns. SQL Loader provides a powerful and efficient way to load large amounts of data into Oracle databases.

#oracle #SQLLoader