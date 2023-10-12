---
layout: post
title: "Loading data into tables with column defaults using SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

When using SQL Loader to load data into an Oracle database table, you may encounter situations where certain columns have default values defined. These default values are automatically assigned to the columns if no value is provided in the input data file. In this blog post, we will discuss how to load data into tables with column defaults using SQL Loader.

## Table Structure

Let's consider a simple example where we have a table called `employees` with the following structure:

```sql
CREATE TABLE employees (
  id NUMBER,
  name VARCHAR2(50) DEFAULT 'Unknown',
  salary NUMBER DEFAULT 0,
  hire_date DATE DEFAULT SYSDATE
);
```

In this table, the `name` column has a default value of 'Unknown', the `salary` column has a default value of 0, and the `hire_date` column has a default value of the current system date.

## Input Data File

Assuming we have an input data file called `employees.csv` containing the following data:

```csv
1001,John Doe,5000,2021-01-01
1002,Jane Smith,,2021-03-15
1003,Adam Johnson,3000,
```

In this example, the second row doesn't provide a value for the `salary` column, and the third row doesn't provide a value for the `hire_date` column.

## SQL Loader Control File

To load the data from the `employees.csv` file into the `employees` table, we need to create a SQL Loader control file, let's call it `load.ctl`, with the following content:

```plaintext
OPTIONS (SKIP=1)
LOAD DATA
INFILE 'employees.csv'
INTO TABLE employees
APPEND
FIELDS TERMINATED BY ','
TRAILING NULLCOLS
(
  id,
  name,
  salary DEFAULT NULL,
  hire_date "YYYY-MM-DD" DEFAULT sysdate
)
```

In this control file, we specify the input file, the target table, and the delimiter used in the CSV file (',' in this case). For the columns with default values, we use the `DEFAULT` keyword to instruct SQL Loader to assign the default value if no value is provided.

## Loading Data with SQL Loader

To load data into the `employees` table using SQL Loader, you can run the following command:

```bash
sqlldr username/password@database control=load.ctl log=load.log
```

Replace `username`, `password`, and `database` with your actual credentials and database details. This command instructs SQL Loader to use the control file `load.ctl` and logs the load process into `load.log`.

## Conclusion

Loading data into tables with column defaults using SQL Loader is a straightforward process. By specifying the `DEFAULT` keyword in the SQL Loader control file, you can ensure that columns with default values are populated automatically if no value is provided in the input data file. This feature can save you time and effort when loading large datasets into your Oracle database.