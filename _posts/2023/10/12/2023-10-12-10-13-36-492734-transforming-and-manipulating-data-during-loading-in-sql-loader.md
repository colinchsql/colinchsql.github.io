---
layout: post
title: "Transforming and manipulating data during loading in SQL Loader."
description: " "
date: 2023-10-12
tags: [sqlloader, dataimport]
comments: true
share: true
---

When using SQL Loader to load data into an Oracle database, you may often need to transform or manipulate the data before it is inserted into the tables. This can involve simple tasks like converting data types or more complex tasks like applying business rules to the data.

Fortunately, SQL Loader provides several features that allow you to perform these transformations and manipulations during the loading process. In this blog post, we will explore some of these features and how you can leverage them to handle your data loading requirements.

## 1. Using SQL Expressions

SQL Loader allows you to use SQL expressions to manipulate the data as it is loaded. You can specify these SQL expressions using the `FIELDS` clause in your control file. 

For example, let's say you have a column `price` in your input file that contains the data in cents, but you want to load it into a table with the data in dollars. You can achieve this by using the `SQL` keyword in the control file, as shown below:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE my_table
FIELDS TERMINATED BY ','
(price "TO_NUMBER(:price) / 100")
```

In the above example, the SQL expression `TO_NUMBER(:price) / 100` is applied to the `price` field during loading, converting it from cents to dollars.

## 2. Using Functions

In addition to SQL expressions, SQL Loader also provides built-in functions that you can use to manipulate the data during loading. These functions can be used within the control file to transform the data according to your requirements.

For instance, suppose you have a column `name` in your input file that is in uppercase, but you want to load it in title case. You can achieve this by using the `LOWER` and `INITCAP` functions in the control file, as shown below:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE my_table
FIELDS TERMINATED BY ','
(name "INITCAP(LOWER(:name))")
```

In the above example, the `LOWER` function is used to convert the `name` field to lowercase, and then the `INITCAP` function is applied to convert the first character of each word to uppercase, resulting in the data being loaded in title case.

## 3. Conditional Loading

SQL Loader also allows you to conditionally load data based on specific criteria. This can be accomplished using the `WHEN` clause in the control file.

Let's say you have a column `status` in your input file, and you only want to load the records where the status is "ACTIVE". You can achieve this by using the `WHEN` clause as shown below:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE my_table
FIELDS TERMINATED BY ','
WHEN status = 'ACTIVE'
```

In the above example, only the records with the status "ACTIVE" will be loaded into the table, while the rest will be ignored.

## 4. Multitable and Joins

If you have a more complex data loading requirement where you need to load data into multiple tables or perform joins during loading, SQL Loader provides the `INTO TABLE` clause and the `APPEND` keyword.

You can specify multiple tables in the control file and use the `APPEND` keyword to add records to those tables. This allows you to perform joins and load data into related tables.

```sql
LOAD DATA
INFILE 'data.csv'
APPEND
INTO TABLE customers
...
INTO TABLE orders
...
```

In the above example, data from the input file will be loaded into both the `customers` and `orders` tables in the database.

## Conclusion

SQL Loader is a powerful tool for loading data into an Oracle database, and its ability to transform and manipulate data during the loading process makes it even more flexible. By utilizing SQL expressions, functions, conditional loading, and the ability to load data into multiple tables, you can handle complex data loading requirements efficiently.

Whether you need to convert data types, apply business rules, or perform joins, SQL Loader provides the necessary features to accomplish these tasks. Experiment with these features in your next data loading project to streamline your data loading process and ensure data accuracy.

#sqlloader #dataimport