---
layout: post
title: "SQL LAST_VALUE with table type"
description: " "
date: 2023-09-29
tags: [TableType]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in a set of values. This can be especially useful when working with table types in SQL, where you may need to extract the last value from a specific column.

Here is an example of how the `LAST_VALUE` function can be used with a table type:

```sql
-- Create a table type
CREATE TYPE EmployeeTable AS TABLE
(
    EmployeeID INT,
    EmployeeName VARCHAR(50),
    JoiningDate DATE
);

-- Declare a variable of the table type
DECLARE @Employees EmployeeTable;

-- Insert sample data into the table variable
INSERT INTO @Employees (EmployeeID, EmployeeName, JoiningDate)
VALUES
    (1, 'John Doe', '2021-01-01'),
    (2, 'Jane Smith', '2021-02-15'),
    (3, 'Mike Johnson', '2021-03-10');

-- Retrieve the last joining date using LAST_VALUE
SELECT DISTINCT
    EmployeeID,
    EmployeeName,
    LAST_VALUE(JoiningDate) OVER (ORDER BY EmployeeID) AS LastJoiningDate
FROM
    @Employees;
```

In the above example, we first create a table type called `EmployeeTable` with three columns: `EmployeeID`, `EmployeeName`, and `JoiningDate`. We then declare a variable `@Employees` of this table type and insert some sample data into it.

Next, we use the `LAST_VALUE` function with the `OVER` clause to retrieve the last joining date for each employee. The `LAST_VALUE` function is applied on the `JoiningDate` column and is ordered by the `EmployeeID`. The result is returned with distinct `EmployeeID`, `EmployeeName`, and the last joining date.

By using the `LAST_VALUE` function in conjunction with table types, we can easily extract the last value from a specific column within the table type. This can be helpful in various scenarios, such as finding the most recent date or the latest record inserted in a table type.

#SQL #TableType