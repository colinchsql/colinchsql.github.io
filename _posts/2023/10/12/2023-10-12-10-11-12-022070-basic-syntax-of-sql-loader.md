---
layout: post
title: "Basic syntax of SQL Loader."
description: " "
date: 2023-10-12
tags: [oracle]
comments: true
share: true
---

SQL Loader is a powerful command-line tool provided by Oracle for loading data into Oracle database tables from external files. It is a useful utility for efficiently importing large volumes of data into Oracle databases.

The basic syntax of SQL Loader is as follows:

```sql
sqlldr <username>/<password>@<database> <control_file>
```

Let's break down the different components of the syntax:

- `<username>`: The username used to access the Oracle database.
- `<password>`: The password associated with the username.
- `<database>`: The TNS database string or Easy Connect string that identifies the database to load the data into.
- `<control_file>`: The name of the control file that contains the instructions for SQL Loader on how to load the data.

The control file is a vital component of the SQL Loader as it specifies various parameters and settings used during the data loading process. It defines the source file, target table, field mappings, formatting options, and more.

Here's a basic example of a control file:

```sql
LOAD DATA
INFILE 'data.csv' -- Input data file
APPEND INTO TABLE employees -- Target table

FIELDS TERMINATED BY ',' -- Field delimiter in data file
OPTIONALLY ENCLOSED BY '"'

(emp_id,
 emp_name,
 emp_salary)
```

In this example, `data.csv` is the input file containing the data to be loaded. The data will be appended to the `employees` table. The fields in the data file are separated by commas and are optionally enclosed by double quotation marks.

The control file further specifies the mapping of fields from the data file to columns in the table. In this case, the control file expects three fields: `emp_id`, `emp_name`, and `emp_salary`.

Once you have your control file defined, you can execute the SQL Loader command to load the data into the Oracle database.

SQL Loader is a versatile tool with various options and features, allowing you to customize the data loading process to meet your specific requirements. You can explore the official Oracle documentation for a comprehensive understanding of SQL Loader's capabilities.

#sql #oracle