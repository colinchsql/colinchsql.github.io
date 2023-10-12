---
layout: post
title: "Loading data from a CSV file using SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

CSV (Comma-Separated Values) files are a popular format for storing tabular data. When working with a large amount of data, it can be much more efficient to load the data into a database rather than processing it in memory or multiple files. SQL*Loader is a utility provided by Oracle to load data from external files into Oracle databases.

In this tutorial, we will walk through the steps to load data from a CSV file into an Oracle database using SQL Loader.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Step 1: Create a Control File](#step-1-create-a-control-file)
- [Step 2: Create a Table](#step-2-create-a-table)
- [Step 3: Create a CSV File](#step-3-create-a-csv-file)
- [Step 4: Load Data Using SQL Loader](#step-4-load-data-using-sql-loader)
- [Conclusion](#conclusion)

## Prerequisites
Before we start, make sure you have the following:

- [Oracle Database](https://www.oracle.com/database/) installed and running
- Access to the SQL*Loader utility (usually comes with Oracle Database)
- A text editor to create control files

## Step 1: Create a Control File
The control file is a text file that defines how the data from the CSV file should be loaded into the database. It specifies the location of the CSV file, the character set, the table name, and the column mappings.

Here is an example control file named `mydata.ctl`:

```sql
LOAD DATA
INFILE 'mydata.csv'
BADFILE 'mydata.bad'
DISCARDFILE 'mydata.dsc'
APPEND
INTO TABLE employees
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
TRAILING NULLCOLS
(
  id,
  name,
  age,
  salary
)
```

In this example:
- `LOAD DATA`: Specifies that we are loading data.
- `INFILE 'mydata.csv'`: Specifies the location of the CSV file.
- `BADFILE 'mydata.bad'`: Specifies the name of the bad file, which contains records that could not be loaded due to errors.
- `DISCARDFILE 'mydata.dsc'`: Specifies the name of the discard file, which contains records that were discarded during loading.
- `APPEND`: Specifies that the data should be appended to the existing table.
- `INTO TABLE employees`: Specifies the name of the table where the data should be loaded.
- `FIELDS TERMINATED BY ','`: Specifies that the fields in the CSV file are separated by commas.
- `OPTIONALLY ENCLOSED BY '"'`: Specifies that the fields in the CSV file are optionally enclosed by double quotes.
- `TRAILING NULLCOLS`: Specifies that any trailing null columns should be considered as null values.

## Step 2: Create a Table
Before loading data, we need to create a table in the database that will hold the data. Here is an example SQL statement to create a table named `employees`:

```sql
CREATE TABLE employees (
  id NUMBER,
  name VARCHAR2(50),
  age NUMBER,
  salary NUMBER
);
```

Make sure the table structure matches the columns specified in the control file.

## Step 3: Create a CSV File
Next, create a CSV file containing the data you want to load. The data should be in the same order as the column definitions in the table.

For example, create a file named `mydata.csv` with the following content:

```csv
1,John Doe,30,50000
2,Jane Smith,35,60000
3,James Johnson,40,70000
```

## Step 4: Load Data Using SQL Loader
Once you have the control file, table, and CSV file ready, you can load the data using SQL Loader. Open the command prompt or terminal and run the following command:

```
sqlldr username/password control=mydata.ctl log=mydata.log
```

Replace `username` and `password` with your Oracle database username and password.

SQL Loader will read the control file and load the data from the CSV file into the specified table. The progress and any errors will be logged to the specified log file (`mydata.log` in this example).

## Conclusion
Loading data from a CSV file into an Oracle database using SQL Loader is a straightforward process. By following the steps outlined in this tutorial, you can efficiently load large amounts of data and leverage the power of a relational database for data analysis and processing.

Remember to create the control file, table, and CSV file correctly, and ensure that the column mappings are accurate.