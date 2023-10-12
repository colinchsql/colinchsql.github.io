---
layout: post
title: "Skipping header rows in SQL Loader."
description: " "
date: 2023-10-12
tags: [data, sqlloader]
comments: true
share: true
---

In the world of data loading and importing, SQL Loader is a popular tool used to efficiently load data from external files into an Oracle database. However, many times these files contain header rows that need to be skipped before the actual data is loaded. In this blog post, we will explore how to skip header rows in SQL Loader and streamline the data loading process.

## What are Header Rows?

Header rows are often included in data files to provide column names or a description of the data. While these header rows are useful for human readability, they can cause issues when it comes to loading the data into a database. Loading the header rows along with the actual data can result in data integrity issues and unexpected errors.

## Using SKIP Parameter

SQL Loader provides a **SKIP** parameter that allows you to skip a specified number of rows at the beginning of the data file. This parameter tells SQL Loader to ignore these rows and start loading data from the subsequent rows.

Here's an example of how to use the **SKIP** parameter in the control file:

```sql
LOAD DATA
INFILE 'data.csv'
APPEND INTO TABLE my_table
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
TRAILING NULLCOLS
(SKIP 1
  column1,
  column2,
  column3
)
```

In the above example, the **SKIP** parameter is set to 1, indicating that one row should be skipped before starting the data loading process. You can adjust the number depending on the number of header rows present in your data file.

## Dynamic SKIP Based on Content

In some cases, the number of header rows can vary from file to file. To handle such dynamic scenarios, you can make use of SQL Loader's **LOAD WHEN** clause along with a condition to skip rows based on the content.

Here's an example:

```sql
LOAD DATA
INFILE 'data.csv'
APPEND INTO TABLE my_table
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
TRAILING NULLCOLS
(LOAD WHEN (1:5) <> 'Header'
  column1,
  column2,
  column3
)
```

In the above example, the **LOAD WHEN** clause is used to check if the first five characters of a row are not equal to 'Header'. If the condition is met, SQL Loader proceeds with loading the row, effectively skipping any rows that start with 'Header'.

## Conclusion

Skipping header rows in SQL Loader can greatly simplify the data loading process by avoiding issues related to data integrity and errors. By utilizing the **SKIP** parameter or dynamically skipping rows based on their content, you can efficiently import data files into your Oracle database.

Remember to adjust the **SKIP** value or condition based on the number of header rows and their content in your specific data files. Happy data loading!

#data #sqlloader