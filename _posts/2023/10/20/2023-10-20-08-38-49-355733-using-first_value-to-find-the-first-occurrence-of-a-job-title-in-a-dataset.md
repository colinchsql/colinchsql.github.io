---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a job title in a dataset"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When working with datasets, it is often necessary to find the first occurrence of a specific value within a group. In SQL, the `FIRST_VALUE` function can be used to retrieve the first value in a sorted partition of data. In this blog post, we will explore how to use `FIRST_VALUE` to find the first occurrence of a job title in a dataset.

## Table of Contents
- [Introduction](#introduction)
- [Syntax](#syntax)
- [Example](#example)
- [Conclusion](#conclusion)

## Introduction

The `FIRST_VALUE` function is a window function in SQL that allows you to retrieve the first value in an ordered set of data based on a given criteria. It is often used in combination with the `PARTITION BY` clause, which divides the dataset into separate groups.

## Syntax

The syntax for using `FIRST_VALUE` is as follows:

```sql
FIRST_VALUE(expression) OVER (
  [PARTITION BY column1, column2, ...]
  ORDER BY column [ASC|DESC]
  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) AS first_value
```

- `expression` represents the column or expression from which the first value should be retrieved.
- `PARTITION BY` is an optional clause that divides the dataset into separate groups. The first value is determined within each group.
- `ORDER BY` specifies the column by which the dataset should be sorted.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` is a required clause that sets the window frame for the `FIRST_VALUE` function.

## Example

Let's consider a sample dataset of employees:

| ID | Name   | Job Title    | Salary |
|----|--------|--------------|--------|
| 1  | John   | Developer    | 5000   |
| 2  | Jane   | Analyst      | 4500   | 
| 3  | Mark   | Manager      | 6000   |
| 4  | Sarah  | Developer    | 5500   |
| 5  | Emily  | Data Scientist| 7000   |

To find the first occurrence of each job title in this dataset, we can use the `FIRST_VALUE` function:

```sql
SELECT DISTINCT
    FIRST_VALUE(Job_Title) OVER (PARTITION BY Job_Title ORDER BY ID) AS first_title
FROM 
    employees;
```

This query will return the following result:

| first_title   |
|---------------|
| Analyst       |
| Data Scientist|
| Developer     |
| Manager       |

The `FIRST_VALUE` function is applied to the `Job_Title` column, and the result is ordered by the `ID` column. By including the `DISTINCT` keyword, we ensure that only the first occurrence of each job title is returned.

## Conclusion

In this blog post, we explored how to use the `FIRST_VALUE` function in SQL to find the first occurrence of a job title in a dataset. By utilizing the `PARTITION BY` and `ORDER BY` clauses, we can easily retrieve the first value within each group. The `FIRST_VALUE` function is a powerful tool for analyzing datasets and can be applied to various scenarios requiring the identification of first occurrences.