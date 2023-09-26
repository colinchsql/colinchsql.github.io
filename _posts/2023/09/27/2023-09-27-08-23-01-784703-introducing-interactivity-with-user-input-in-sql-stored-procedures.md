---
layout: post
title: "Introducing interactivity with user input in SQL stored procedures"
description: " "
date: 2023-09-27
tags: [StoredProcedures]
comments: true
share: true
---

As SQL developers, we often encounter scenarios where we need to interact with the end user and gather input for certain operations. While SQL alone does not provide a native way to collect user input, we can achieve interactivity by utilizing **stored procedures**.

A stored procedure is a set of pre-compiled SQL statements that can be executed repeatedly. It offers the ability to encapsulate complex logic and execute it as a single unit, often improving performance and maintainability. By incorporating user input into our stored procedures, we enable a more interactive and dynamic experience for our users.

## Simple User Input

Let's start by looking at a simple example where we prompt the user to provide a name and then use that input to query a database table. Here's an example in **T-SQL**:

```sql
-- Create a stored procedure
CREATE PROCEDURE GetUserDetails
    @name NVARCHAR(50)
AS
BEGIN
    SELECT * FROM Users WHERE Name = @name;
END

-- Execute the stored procedure with user input
EXEC GetUserDetails 'John Smith';
```

In this example, we define a stored procedure called `GetUserDetails` that takes a parameter `@name`. We use this parameter as a filter in our `SELECT` statement to retrieve user details from the `Users` table. Finally, we execute the stored procedure with the user input `'John Smith'`.

By incorporating user input as parameters in our stored procedures, we gain the ability to customize database operations based on user-provided values.

## Advanced User Interaction

In more complex scenarios, we may want to gather multiple inputs from the user or validate the input before executing database operations. Consider the following example using **PL/SQL**:

```plsql
-- Create a stored procedure
CREATE OR REPLACE PROCEDURE AddNewUser(
    p_name IN VARCHAR2,
    p_email IN VARCHAR2,
    p_age IN NUMBER
)
AS
BEGIN
    -- Validate user inputs
    IF p_age < 18 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Age must be 18 or higher.');
    END IF;

    -- Perform database operations
    INSERT INTO Users (Name, Email, Age) VALUES (p_name, p_email, p_age);
    COMMIT;
    DBMS_OUTPUT.PUT_LINE('New user added successfully.');
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
        ROLLBACK;
END;
/

-- Execute the stored procedure with user input
BEGIN
    EXEC AddNewUser('Jane Doe', 'jane@example.com', 21);
    COMMIT;
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
        ROLLBACK;
END;
```

In this example, we define a stored procedure called `AddNewUser` that takes three parameters: `p_name`, `p_email`, and `p_age`. We validate the `p_age` parameter to ensure it's greater than or equal to 18. If the validation fails, an exception is raised with a custom error message. Otherwise, the procedure performs an `INSERT` operation to add a new user to the `Users` table.

By incorporating user input as parameters and adding validation logic, we can create more robust stored procedures that handle user interactions effectively.

## Conclusion

By incorporating user input into SQL stored procedures, we can introduce interactivity and make our database operations more dynamic. With the ability to gather user input and perform operations based on those inputs, we can create powerful and flexible solutions. Remember to handle user input carefully to prevent SQL injection attacks and to provide a smooth user experience.

#SQL #StoredProcedures