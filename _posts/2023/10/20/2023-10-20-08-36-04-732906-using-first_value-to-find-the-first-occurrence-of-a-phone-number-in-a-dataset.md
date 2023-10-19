---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a phone number in a dataset"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In data analysis and processing, it is often necessary to find the first occurrence of a specific value in a dataset. This becomes especially relevant when dealing with large datasets where identifying the first occurrence of a particular value is crucial. One common scenario is finding the first occurrence of a phone number in a dataset.

In SQL, you can use the `FIRST_VALUE` function to accomplish this task. `FIRST_VALUE` is an analytical function that returns the first value in an ordered set of values.

## Syntax

The syntax for using `FIRST_VALUE` is as follows:

```sql
FIRST_VALUE(expression) OVER (
    [PARTITION BY partition_expression]
    ORDER BY sort_expression
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) 
```

The key components of this syntax are:

- `expression`: The value you want to retrieve the first occurrence of.
- `PARTITION BY`: (Optional) If you want to partition the dataset by a specific column before finding the first value, you can specify it here.
- `ORDER BY`: The column you want to order the dataset by in order to determine the first value.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: This specifies the range of rows to consider when determining the first value.

## Example

Let's say we have a dataset named `contacts` with the following columns: `contact_id`, `name`, and `phone_number`.

| contact_id | name        | phone_number  |
|------------|-------------|---------------|
| 1          | John Doe    | 123-456-7890  |
| 2          | Jane Smith  | 555-123-4567  |
| 3          | Alex Johnson| 987-654-3210  |
| 4          | Sarah Adams | 555-789-1234  |

To find the first occurrence of a phone number in this dataset, we can use the following SQL query:

```sql
SELECT DISTINCT
    FIRST_VALUE(phone_number) OVER (
        ORDER BY contact_id
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS first_phone_number
FROM
    contacts;
```

This query will return the result:

| first_phone_number |
|--------------------|
| 123-456-7890       |
| 123-456-7890       |
| 123-456-7890       |
| 123-456-7890       |

In this example, we use `FIRST_VALUE` to find the first occurrence of the `phone_number` column. The dataset is ordered by the `contact_id` column, ensuring that the first phone number is retrieved for each row.

## Conclusion

Using `FIRST_VALUE` in SQL allows us to easily find the first occurrence of a specific value in a dataset. In the case of finding the first occurrence of a phone number, this function is particularly useful. By utilizing the `ORDER BY` clause, we can determine the first value based on a specific column. This can be a valuable tool for data analysis and processing tasks.