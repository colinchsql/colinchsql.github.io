---
layout: post
title: "Executing stored procedures in SQL CLI"
description: " "
date: 2023-10-16
tags: [SQLCLI, StoredProcedures]
comments: true
share: true
---

In this blog post, we will explore how to execute stored procedures using the SQL Command Line Interface (CLI). Stored procedures are precompiled blocks of SQL statements that can be executed with a single call. They are commonly used to encapsulate complex logic and perform repetitive tasks in a database.

## Connecting to the Database

Before we can execute a stored procedure, we need to establish a connection to the database. Assuming you have already installed the SQL CLI and have the necessary credentials, follow these steps:

1. Open the command prompt or terminal.
2. Type `sql-cli` to launch the SQL CLI.
3. Enter the database connection details in the prompt, such as the server address, username, and password.

Once you are connected, you can start executing SQL queries and commands, including stored procedures.

## Executing a Stored Procedure

To execute a stored procedure in SQL CLI, we use the `EXEC` keyword followed by the procedure name. Here is an example:

```sql
EXEC usp_GetEmployeeDetails;
```

In the above example, `usp_GetEmployeeDetails` is the name of the stored procedure we want to execute. Make sure to replace it with the actual name of the procedure you want to execute.

## Passing Parameters to the Stored Procedure

Stored procedures often accept parameters to perform specific actions or filter data. To pass parameters when executing a stored procedure in SQL CLI, we use the `EXEC` statement followed by the procedure name and the parameter values:

```sql
EXEC usp_GetEmployeeDetails @EmployeeId = 123;
```

In the above example, `@EmployeeId` is a parameter of the stored procedure `usp_GetEmployeeDetails`, and we are passing the value `123` to it. Adjust the parameter name and value according to the stored procedure you want to execute.

## Conclusion

In this blog post, we learned how to execute stored procedures using the SQL Command Line Interface (CLI). We covered connecting to the database, executing stored procedures, and passing parameters to them. Now you are ready to leverage the power of stored procedures in your SQL CLI workflow.

If you found this post helpful, feel free to share it on social media with the hashtag #SQLCLI and #StoredProcedures. Happy coding!

References:
- [SQL Command Line Interface (CLI) documentation](https://docs.microsoft.com/sql/tools/sqlcmd-utility)
- [Stored Procedures in SQL Server](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine)