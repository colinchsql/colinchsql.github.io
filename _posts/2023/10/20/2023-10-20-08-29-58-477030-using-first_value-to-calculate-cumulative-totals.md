---
layout: post
title: "Using FIRST_VALUE to calculate cumulative totals"
description: " "
date: 2023-10-20
tags: [GUID]
comments: true
share: true
---

Cumulative totals are a common requirement when analyzing data, especially in finance or sales. Calculating cumulative totals involves summing up a value repeatedly, as each row is processed.

One way to achieve this in SQL is by using the `FIRST_VALUE()` function. This function allows us to access the value of a specified column from the first row of a partition.

Let's consider a table `sales` with the following schema:

```sql
CREATE TABLE sales (
    date DATE,
    amount INT
);
```

To calculate the cumulative sales amount for each date, we can use the following query:

```sql
SELECT
    date,
    SUM(amount) OVER (
        ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS cumulative_total
FROM sales;
```

In this query, we use the `SUM()` function along with the `OVER` clause. The `ORDER BY date` ensures that the calculation is done in ascending order of dates. The `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` clause specifies that we want the sum from the first row up to the current row.

The `FIRST_VALUE()` function is implicitly used here when we specify `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. It fetches the value of `amount` from the first row within the partition (all rows in this case) for each row.

The result of the query would be a result set with the date and the cumulative total for each date.

For example:

|   date    | cumulative_total |
|-----------|-----------------|
| 2022-01-01|       100       |
| 2022-01-02|       230       |
| 2022-01-03|       540       |
| 2022-01-04|       860       |

By utilizing the `FIRST_VALUE()` function and the `OVER` clause with the appropriate `ROWS BETWEEN` specification, we can easily calculate cumulative totals in SQL.

This technique can be extended to perform various calculations and analysis on cumulative data, such as identifying peaks, trends, or forecasting.

# References
- [Oracle Documentation on FIRST_VALUE](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.htm#GUID-D3EA49F9-FB9C-45EE-A0DA-27169A6AFC21)
- [Microsoft SQL Server Documentation on FIRST_VALUE](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)