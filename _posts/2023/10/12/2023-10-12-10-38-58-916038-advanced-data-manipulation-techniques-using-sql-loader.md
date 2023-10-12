---
layout: post
title: "Advanced data manipulation techniques using SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

SQL Loader is a powerful tool provided by Oracle for loading data into a database table efficiently. It allows you to perform various data manipulation tasks during the loading process. In this article, we will explore some advanced data manipulation techniques using SQL Loader.

## Table of Contents
- [Introduction to SQL Loader](#introduction-to-sql-loader)
- [Data Transformation](#data-transformation)
   - [Using SQL Expressions](#using-sql-expressions)
   - [Skipping Columns](#skipping-columns)
- [Conditional Loading](#conditional-loading)
   - [Using WHEN Clause](#using-when-clause)
   - [Using NULLIF Clause](#using-nullif-clause)
- [Validation and Rejection](#validation-and-rejection)
   - [Using USING Clause](#using-using-clause)
   - [Using REJECT Clause](#using-reject-clause)
- [Conclusion](#conclusion)

## Introduction to SQL Loader

SQL Loader is a utility provided by Oracle that enables high-speed data loading from external files into Oracle database tables. It uses a control file to specify the input data format and provides various options to manipulate the data during the loading process.

## Data Transformation

### Using SQL Expressions

SQL Loader allows you to perform transformations on the data being loaded using SQL expressions. You can use functions, operators, and SQL statements to manipulate the data. For example, you can convert a string to uppercase, format dates, or extract substrings from a column value.

To perform data transformation using SQL expressions, you can use the `FIELDS` clause in the control file. This clause enables you to specify the column name followed by the SQL expression to transform the data.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id,
  emp_name,
  emp_salary EXPRESSION "TO_NUMBER(emp_salary) * 1.1"
)
```

In the above example, the `emp_salary` column value will be multiplied by 1.1 during the loading process.

### Skipping Columns

Sometimes, you may have input data files that contain extra columns that are not required for loading into the database table. SQL Loader allows you to skip these columns during the loading process.

To skip a column, you can use the `FILLER` keyword in the control file. This keyword instructs SQL Loader to ignore the specified column in the input file.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id,
  FILLER,
  emp_name,
  emp_salary
)
```

In the above example, the second column in the input file will be skipped during the loading process.

## Conditional Loading

### Using WHEN Clause

SQL Loader provides the `WHEN` clause, which allows you to conditionally load data based on a specific condition. You can specify a condition using logical operators and comparison operators in the control file.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id,
  emp_name,
  emp_salary
)
WHEN emp_salary > 1000
```

In the above example, only the rows with an `emp_salary` greater than 1000 will be loaded into the database table.

### Using NULLIF Clause

The `NULLIF` clause is another powerful feature of SQL Loader that allows you to set specific values as null during the loading process. It is useful when you have default values or special characters in the data that need to be treated as null.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id,
  emp_name,
  emp_salary NULLIF emp_salary=9999
)
```

In the above example, if the `emp_salary` value is 9999, it will be loaded as null in the database table.

## Validation and Rejection

### Using USING Clause

SQL Loader provides the `USING` clause, which allows you to perform validation checks on the loaded data. You can specify a condition using logical operators and comparison operators to validate the data before loading it into the database table.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id INTEGER EXTERNAL,
  emp_name,
  emp_salary INTEGER EXTERNAL
)
USING emp_salary < 10000
```

In the above example, only the rows with an `emp_salary` less than 10000 will be loaded into the database table.

### Using REJECT Clause

The `REJECT` clause in SQL Loader allows you to specify a separate file to store the rejected records during the loading process. This is helpful when you want to keep track of the records that failed validation or encountered errors.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
  emp_id INTEGER EXTERNAL,
  emp_name,
  emp_salary INTEGER EXTERNAL
)
REJECT LIMIT 5
```

In the above example, up to 5 rejected records will be stored in a separate file specified by the `REJECT` clause.

## Conclusion

SQL Loader provides advanced data manipulation techniques that enable you to perform transformations, conditional loading, and validation checks during the data loading process. By utilizing these techniques, you can effectively load and manipulate data from external files into the Oracle database table.