---
layout: post
title: "Generating random data in SQL CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

When working with SQL (Structured Query Language), there may be situations where you need to generate random data for testing or demonstration purposes. In this blog post, we will explore different techniques to generate random data using SQL CLI (Command Line Interface).

## Table of Contents
1. [Generate random numbers](#generate-random-numbers)
2. [Generate random strings](#generate-random-strings)
3. [Generate random dates](#generate-random-dates)

## Generate random numbers

To generate random numbers in SQL CLI, you can make use of the `RAND()` function. This function returns a random decimal value between 0 and 1. By manipulating this value, you can generate random integers within a specific range. Here's an example:

```sql
-- Generate a random integer between 1 and 100
SELECT FLOOR(RAND()*(100-1+1))+1 AS random_number;
```

In the above example, `FLOOR()` function is used to convert the decimal value to an integer. The `RAND()` function generates a random decimal between 0 and 1, which is then multiplied by the range (100-1+1) and added to the minimum value (1).

## Generate random strings

To generate random strings in SQL CLI, you can utilize the `SUBSTRING()` function along with the `RAND()` function. Here's an example of generating a random string of a specific length:

```sql
-- Generate a random string of length 10
SELECT SUBSTRING(MD5(RAND()), 1, 10) AS random_string;
```

In the above example, `MD5()` function is used to generate a random hexadecimal string based on the output of the `RAND()` function. The `SUBSTRING()` function is then used to retrieve the first 10 characters of the generated string.

## Generate random dates

To generate random dates in SQL CLI, you can use the `DATEADD()` function along with the `RAND()` function. Here's an example of generating a random date within a specific range:

```sql
-- Generate a random date between '2021-01-01' and '2021-12-31'
SELECT DATEADD(DAY, FLOOR(RAND()*(DATEDIFF(DAY, '2021-01-01', '2021-12-31')+1)), '2021-01-01') AS random_date;
```

In the above example, `DATEDIFF()` function is used to calculate the number of days between the two specified dates. The `RAND()` function generates a random decimal between 0 and 1, which is then multiplied by the number of days between the dates. Finally, the `DATEADD()` function is used to add the calculated number of days to the minimum date.

## Conclusion

Generating random data in SQL CLI is a useful technique for testing and demonstrating various scenarios. By using the `RAND()` function along with other SQL functions, you can easily generate random numbers, strings, and dates. Experiment with these techniques and adapt them to your specific requirements.

***References:***
- [Microsoft SQL Documentation - RAND](https://docs.microsoft.com/en-us/sql/t-sql/functions/rand-transact-sql?view=sql-server-ver15)
- [Microsoft SQL Documentation - FLOOR](https://docs.microsoft.com/en-us/sql/t-sql/functions/floor-transact-sql?view=sql-server-ver15)
- [Microsoft SQL Documentation - SUBSTRING](https://docs.microsoft.com/en-us/sql/t-sql/functions/substring-transact-sql?view=sql-server-ver15)
- [Microsoft SQL Documentation - DATEADD](https://docs.microsoft.com/en-us/sql/t-sql/functions/dateadd-transact-sql?view=sql-server-ver15)
- [Microsoft SQL Documentation - DATEDIFF](https://docs.microsoft.com/en-us/sql/t-sql/functions/datediff-transact-sql?view=sql-server-ver15)