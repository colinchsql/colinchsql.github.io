---
layout: post
title: "SQL LAST_VALUE with NULLS LAST option"
description: " "
date: 2023-09-28
tags: [nulls]
comments: true
share: true
---

In SQL, the LAST_VALUE function is used to retrieve the last value in a sorted window frame. By default, this function returns the last non-null value in the window frame. However, there may be situations where you want the last value to be null if all values in the window frame are null.

Fortunately, SQL provides the NULLS LAST option that allows you to specify whether null values should appear first or last in the ordering. This option can be used in conjunction with the LAST_VALUE function to achieve the desired behavior.

Let's consider an example to demonstrate the usage of LAST_VALUE with the NULLS LAST option. Suppose we have a "sales" table with the following data:

```
+------+-------+
| Year | Sales |
+------+-------+
| 2018 | 1000  |
| 2019 | NULL  |
| 2020 | 1500  |
| 2021 | NULL  |
+------+-------+
```

To find the last non-null value in the "Sales" column, you can use the following SQL query:

```sql
SELECT 
  Year,
  LAST_VALUE(Sales IGNORE NULLS) OVER (ORDER BY Year ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS Last_Non_Null_Sales
FROM
  sales;
```

The use of `IGNORE NULLS` with LAST_VALUE ensures that only non-null values are considered. This will give us the result:

```
+------+--------------------+
| Year | Last_Non_Null_Sales |
+------+--------------------+
| 2018 |        1000        |
| 2019 |        1500        |
| 2020 |        1500        |
| 2021 |        1500        |
+------+--------------------+
```

In this case, the value of 1500 is repeated for the "Last_Non_Null_Sales" column because it is the last non-null value.

To include null values as the last value instead, you can use the NULLS LAST option:

```sql
SELECT 
  Year,
  LAST_VALUE(Sales IGNORE NULLS) OVER (ORDER BY Year NULLS LAST ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS Last_Value_With_Nulls_Last
FROM
  sales;
```

This will give us the following result:

```
+------+------------------------+
| Year | Last_Value_With_Nulls_Last |
+------+------------------------+
| 2018 |           1000           |
| 2019 |           1500           |
| 2020 |           1500           |
| 2021 |           NULL           |
+------+------------------------+
```

As you can see, the last value is now null since it appears last based on the NULLS LAST option.

In conclusion, the NULLS LAST option can be used with the LAST_VALUE function in SQL to control the placement of null values in the ordering. This is particularly useful when you want the last value to be null if all values are null. By using these features in SQL, you can manipulate the results to suit your specific requirements.

#sql #nulls-last