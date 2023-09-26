---
layout: post
title: "Using table-valued parameters in SQL stored procedures"
description: " "
date: 2023-09-27
tags: [StoredProcedures]
comments: true
share: true
---

Table-valued parameters in SQL Server allow you to pass a table as a parameter to a stored procedure. This can be very useful when you need to pass multiple rows of data to a stored procedure without resorting to temporary tables or complex XML manipulation.

Table-valued parameters have been available since SQL Server 2008, and they provide a more efficient and convenient alternative to other methods of passing multiple rows of data to a stored procedure.

## Creating the Table-Valued Parameter Type

To use table-valued parameters, you first need to create a user-defined table type that represents the structure of the table you want to pass as a parameter. This type can be created using the `CREATE TYPE` statement.

Let's say we have a table called `Employees` with columns `Id`, `Name`, and `Salary`. We can create a table type called `EmployeeType` to represent this structure:

```sql
CREATE TYPE EmployeeType AS TABLE
(
    Id int,
    Name varchar(50),
    Salary decimal(10, 2)
);
```

## Defining the Stored Procedure

Once you have defined the table type, you can use it as a parameter in your stored procedure. The stored procedure can then accept a parameter of type `EmployeeType` and use it just like a regular table, including joining it with other tables, filtering rows, or inserting data into other tables.

Here's an example of a stored procedure that accepts a table-valued parameter and inserts the data into a `Employees` table:

```sql
CREATE PROCEDURE InsertEmployees
(
    @Employees EmployeeType READONLY
)
AS
BEGIN
    INSERT INTO Employees (Id, Name, Salary)
    SELECT Id, Name, Salary
    FROM @Employees;
END;
```

## Passing Table-Valued Parameters

To pass a table-valued parameter to a stored procedure, you can create a table variable of the corresponding type, populate it with data, and then pass it as a parameter to the stored procedure.

Here's an example of how you can pass a table-valued parameter to the `InsertEmployees` stored procedure:

```sql
DECLARE @Employees EmployeeType;

INSERT INTO @Employees (Id, Name, Salary)
VALUES (1, 'John Doe', 5000), (2, 'Jane Smith', 6000), (3, 'Bob Anderson', 7000);

EXEC InsertEmployees @Employees;
```

In this example, we declare a table variable `@Employees` of type `EmployeeType`, populate it with three rows of data, and then execute the `InsertEmployees` stored procedure, passing the table variable as a parameter.

## Conclusion

Table-valued parameters provide a convenient and efficient way to pass multiple rows of data to SQL Server stored procedures. By creating a user-defined table type and using it as a parameter, you can simplify your code and improve performance when working with bulk data operations in SQL Server.

#SQL #StoredProcedures