---
layout: post
title: "Loading data into tables with composite unique keys using SQL Loader."
description: " "
date: 2023-10-12
tags: [database, dataloading]
comments: true
share: true
---

In this blog post, we will explore how to load data into tables that have composite unique keys using SQL Loader. A composite unique key is a combination of two or more columns that uniquely identify a row in a table.

## What is SQL Loader?

SQL Loader is a utility provided by Oracle to efficiently load data from external files into Oracle Database tables. It is capable of handling large volumes of data and supports various data formats.

## Scenario

Let's consider a scenario where we have a table called "employees" with the following columns:

- employee_id (numeric data type)
- department_id (numeric data type)
- employee_name (varchar2 data type)

The requirement is to load data into this table using a CSV file named "employees.csv". The employee_id and department_id combination should be unique for each row.

## Steps to load data with composite unique keys using SQL Loader

### Step 1: Create the control file

First, we need to create a control file that defines how the data in the CSV file should be loaded into the table. Create a file named "employees.ctl" with the following contents:

```
LOAD DATA
INFILE 'employees.csv'
APPEND
INTO TABLE employees
FIELDS TERMINATED BY ','
TRAILING NULLCOLS
(
  employee_id,
  department_id,
  employee_name
)
```

In this control file, we specify the name of the input file (employees.csv), the table to load the data into (employees), the field delimiter (','), and the columns in the table that correspond to the fields in the CSV file.

### Step 2: Prepare the CSV file

Make sure the CSV file (employees.csv) contains the data you want to load into the table. The data should be in the same order as specified in the control file.

Here's an example of how the contents of the employees.csv file should look:

```
1234,10,John Doe
5678,20,Jane Smith
9012,30,Michael Johnson
```

### Step 3: Run SQL Loader

To run SQL Loader, open a command prompt or terminal and navigate to the directory where the control file and CSV file are located.

Run the following command:

```
sqlldr username/password control=employees.ctl
```

Replace "username" and "password" with your Oracle Database credentials. This command tells SQL Loader to use the control file (employees.ctl) to load data into the employees table.

### Step 4: Verify the data

After running SQL Loader, you can verify that the data has been successfully loaded into the employees table by querying the table:

```sql
SELECT * FROM employees;
```

If the data has been loaded correctly, you should see the rows from the CSV file in the result.

## Conclusion

Loading data into tables with composite unique keys can be easily accomplished using SQL Loader. By following the steps outlined in this blog post, you can efficiently load data from external files into Oracle Database tables that have composite unique keys.

Remember to create a control file that defines the data loading process, prepare the CSV file with the data in the correct order, and run SQL Loader with the appropriate command.

#database #dataloading