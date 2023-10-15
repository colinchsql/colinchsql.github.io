---
layout: post
title: "Using relationships (joins) in SQL CLI"
description: " "
date: 2023-10-16
tags: [joins]
comments: true
share: true
---

SQL (Structured Query Language) is a powerful tool for querying and manipulating data within databases. One of the key features of SQL is the ability to combine data from multiple tables using relationships. These relationships, commonly referred to as joins, allow you to link data based on common columns.

In this blog post, we will explore how to use relationships (joins) in SQL CLI (Command-Line Interface). We will cover different types of joins and provide examples to illustrate their usage.

## Table of Contents
- [Inner Join](#inner-join)
- [Left Join](#left-join)
- [Right Join](#right-join)
- [Full Outer Join](#full-outer-join)
- [Conclusion](#conclusion)

## Inner Join
An inner join returns records that have matching values in both tables. It selects rows from both tables where the join condition is met.

To perform an inner join in SQL CLI, you can use the `JOIN` keyword followed by the table name and the `ON` keyword to specify the join condition.

```sql
SELECT *
FROM table1
JOIN table2 ON table1.column = table2.column;
```

## Left Join
A left join returns all records from the left table and the matched records from the right table. If no match is found, NULL values are returned for the right table columns.

To perform a left join in SQL CLI, use the `LEFT JOIN` keywords instead of `JOIN`.

```sql
SELECT *
FROM table1
LEFT JOIN table2 ON table1.column = table2.column;
```

## Right Join
A right join returns all records from the right table and the matched records from the left table. If no match is found, NULL values are returned for the left table columns.

To perform a right join in SQL CLI, use the `RIGHT JOIN` keywords instead of `JOIN`.

```sql
SELECT *
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

## Full Outer Join
A full outer join returns all records when there is a match in either the left or right table. If there is no match, NULL values are returned.

To perform a full outer join in SQL CLI, use the `FULL OUTER JOIN` keywords.

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2 ON table1.column = table2.column;
```

## Conclusion
Using relationships (joins) in SQL CLI allows you to combine data from multiple tables based on common columns. This enables you to extract meaningful insights and perform complex data analysis.

In this blog post, we covered different types of joins including inner join, left join, right join, and full outer join, along with their respective SQL CLI syntax. You can choose the appropriate join type based on your specific data requirements.

Remember to practice and explore various SQL joins to enhance your data manipulation skills. Happy querying!

#hashtags: #SQL #joins