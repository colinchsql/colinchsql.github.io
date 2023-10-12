---
layout: post
title: "Specifying data transformations and mappings in SQL Loader."
description: " "
date: 2023-10-12
tags: [SQLLoader, DataTransformations]
comments: true
share: true
---

SQL Loader is a powerful tool in Oracle Database that allows for efficient loading of data from external files into database tables. It provides features for specifying field transformations and mappings to ensure that the loaded data conforms to the desired format and structure within the database. In this article, we will explore how to specify data transformations and mappings in SQL Loader.

## Table of Contents
- [Data Transformations](#data-transformations)
    - [Character Transformations](#character-transformations)
    - [Numeric Transformations](#numeric-transformations)
- [Data Mapping](#data-mapping)
- [Conclusion](#conclusion)

## Data Transformations
Transformations in SQL Loader can be applied to both character and numeric fields. These transformations allow for the manipulation and conversion of data before it is loaded into the database.

### Character Transformations
Character transformations in SQL Loader allow for common text manipulation operations, such as converting the case of characters, trimming leading or trailing spaces, and replacing characters or substrings.

Here is an example of specifying a transformation in the control file:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
    emp_id,
    emp_name CHAR(20) "UPPER(:emp_name)",
    emp_email CONSTANT 'example@gmail.com',
    emp_phone "TRANSLATE(:emp_phone, '()- ', '')"
)
```

In the above example:
- `UPPER(:emp_name)` converts the `emp_name` field to uppercase before loading it into the database.
- `CONSTANT 'example@gmail.com'` assigns a constant value to the `emp_email` field during the loading process.
- `"TRANSLATE(:emp_phone, '()- ', '')"` removes all parentheses, hyphens, and spaces from the `emp_phone` field.

### Numeric Transformations
Numeric transformations in SQL Loader allow for operations such as rounding decimal values, truncating values, or performing arithmetic calculations on numeric fields.

Here is an example of specifying a numeric transformation in the control file:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
    emp_id,
    emp_salary "ROUND(:emp_salary, 2)",
    emp_bonus "CASE WHEN :emp_bonus > 0 THEN :emp_bonus ELSE 0 END"
)
```

In the above example:
- `"ROUND(:emp_salary, 2)"` rounds the `emp_salary` field to 2 decimal places.
- `"CASE WHEN :emp_bonus > 0 THEN :emp_bonus ELSE 0 END"` sets the value of `emp_bonus` to 0 if it is less than or equal to 0.

## Data Mapping
Data mapping in SQL Loader allows for the mapping of source data to target column values based on predefined mappings or conditional logic.

Here is an example of specifying data mapping in the control file:

```sql
LOAD DATA
INFILE 'data.csv'
INTO TABLE employees
FIELDS TERMINATED BY ','
(
    emp_id,
    emp_department "CONSTANT 'HR'",
    emp_gender "DECODE(:emp_gender, 'M', 'Male', 'F', 'Female', 'Other')"
)
```

In the above example:
- `"CONSTANT 'HR'"` assigns a constant value of `'HR'` to the `emp_department` field during the loading process.
- `"DECODE(:emp_gender, 'M', 'Male', 'F', 'Female', 'Other')"` maps the values of `emp_gender` to their corresponding labels, where `'M'` is mapped to `'Male'`, `'F'` is mapped to `'Female'`, and any other value is mapped to `'Other'`.

## Conclusion
SQL Loader provides powerful features for specifying data transformations and mappings during the loading process. By utilizing these features, you can ensure that the loaded data is appropriately transformed and mapped to meet the requirements of your database tables. This results in efficient and accurate data loading, ultimately facilitating better data analysis and decision-making processes.

**Hashtags:** #SQLLoader #DataTransformations