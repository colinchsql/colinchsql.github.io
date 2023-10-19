---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of an invoice number in a dataset"
description: " "
date: 2023-10-20
tags: [References]
comments: true
share: true
---

When working with datasets, it is often necessary to find the first occurrence of a specific value. One common use case is finding the first occurrence of an invoice number in a dataset containing multiple entries for different invoices.

In SQL, you can utilize the `FIRST_VALUE` function to easily retrieve the first occurrence of a value within a dataset. `FIRST_VALUE` is an analytic function that allows you to access the value of a specified expression from the first row of a result set.

Here is an example of how you can use `FIRST_VALUE` to find the first occurrence of an invoice number in a dataset:

```sql
SELECT invoice_number, 
       FIRST_VALUE(invoice_date) OVER (PARTITION BY invoice_number ORDER BY invoice_date) AS first_invoice_date
FROM invoices;
```

* `invoice_number` is the column containing the invoice numbers.
* `invoice_date` is the column containing the corresponding invoice dates.
* `invoices` is the name of the table containing the dataset.

In this example, the `FIRST_VALUE` function is used with the `OVER` clause to specify the partitioning and ordering of the dataset. The `PARTITION BY` clause partitions the dataset by invoice number, ensuring that the first occurrence is calculated separately for each invoice. The `ORDER BY` clause determines the order in which the rows are evaluated within each partition.

The result of the query will include the invoice number and the corresponding first invoice date for each distinct invoice number in the dataset.

By utilizing the `FIRST_VALUE` function, you can easily identify the first occurrence of an invoice number in a dataset, providing valuable insights into your data analysis or reporting workflows.

# Conclusion

Finding the first occurrence of a specific value within a dataset, such as an invoice number, can be achieved using the `FIRST_VALUE` function in SQL. By partitioning and ordering the dataset appropriately, you can retrieve the first value efficiently and accurately. This functionality can be particularly useful in various data analysis and reporting scenarios.

#References
- [SQL FIRST_VALUE documentation](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15) 
- [Analytic Functions in SQL](https://www.sqlshack.com/analytic-functions-in-sql/)