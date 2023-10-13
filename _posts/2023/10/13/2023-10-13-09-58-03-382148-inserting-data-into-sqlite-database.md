---
layout: post
title: "Inserting Data into SQLite Database"
description: " "
date: 2023-10-13
tags: [csharp]
comments: true
share: true
---

SQLite is a popular lightweight database management system that is widely used in mobile and embedded applications. It provides a fast and efficient way to store and query data in a local database file. In this blog post, we will learn how to insert data into an SQLite database using various programming languages.

## Table of Contents
1. [Inserting Data using Python](#python)
2. [Inserting Data using Java](#java)
3. [Inserting Data using C#](#csharp)

## Inserting Data using Python {#python}

Python provides a simple and elegant way to interact with SQLite databases using the `sqlite3` module. Here's an example of how to insert data into an SQLite database in Python:

```python
import sqlite3

# Connect to the database
conn = sqlite3.connect('example.db')

# Create a cursor object
cursor = conn.cursor()

# Define the SQL query
query = "INSERT INTO students (name, age) VALUES (?, ?)"

# Define the data to be inserted
data = ('John Doe', 25)

# Execute the query
cursor.execute(query, data)

# Commit the transaction
conn.commit()

# Close the connection
conn.close()
```

In the above example, we connect to the database using `sqlite3.connect()` and create a cursor object to execute SQL queries. We define the SQL query to insert data into the `students` table and pass the data as parameters to the `execute()` method. Finally, we commit the transaction and close the connection to the database.

## Inserting Data using Java {#java}

To insert data into an SQLite database in Java, we can use the JDBC (Java Database Connectivity) API. Here's an example of how to insert data into an SQLite database in Java:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class Main {
    public static void main(String[] args) {
        // Connect to the database
        try (Connection conn = DriverManager.getConnection("jdbc:sqlite:example.db")) {
            // Define the SQL query
            String query = "INSERT INTO students (name, age) VALUES (?, ?)";

            // Define the data to be inserted
            String name = "John Doe";
            int age = 25;

            // Create a prepared statement
            PreparedStatement stmt = conn.prepareStatement(query);
            stmt.setString(1, name);
            stmt.setInt(2, age);

            // Execute the query
            stmt.executeUpdate();

            // Close the statement
            stmt.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

In the above example, we establish a connection to the database using `DriverManager.getConnection()` and create a prepared statement to execute the SQL query. We set the values of the parameters using `setString()` and `setInt()` methods. Finally, we execute the query using `executeUpdate()` and close the statement.

## Inserting Data using C# {#csharp}

In C#, we can use the ADO.NET library to insert data into an SQLite database. Here's an example of how to perform an insert operation in C#:

```csharp
using System;
using System.Data.SQLite;

public class Program
{
    public static void Main()
    {
        // Connect to the database
        using (SQLiteConnection conn = new SQLiteConnection("Data Source=example.db"))
        {
            conn.Open();

            // Define the SQL query
            string query = "INSERT INTO students (name, age) VALUES (@name, @age)";

            // Define the data to be inserted
            string name = "John Doe";
            int age = 25;

            // Create a command object
            using (SQLiteCommand cmd = new SQLiteCommand(query, conn))
            {
                cmd.Parameters.AddWithValue("@name", name);
                cmd.Parameters.AddWithValue("@age", age);

                // Execute the query
                cmd.ExecuteNonQuery();
            }

            // Close the connection
            conn.Close();
        }
    }
}
```

In the above example, we establish a connection to the database using `SQLiteConnection` and define the SQL query with parameter placeholders. We create a command object and set the values of the parameters using `Parameters.AddWithValue()`. Finally, we execute the query using `ExecuteNonQuery()` and close the connection.

## Conclusion

Inserting data into an SQLite database is a fundamental operation when working with local databases. In this blog post, we learned how to perform insert operations in SQLite using Python, Java, and C#. By understanding these examples, you can easily customize the code to suit your specific requirements and build robust database applications.

**References:**

- [Python SQLite3 Documentation](https://docs.python.org/3/library/sqlite3.html)
- [Java SQLite Tutorial](https://www.sqlitetutorial.net/sqlite-java/)
- [C# SQLite Database Tutorial](https://zetcode.com/csharp/sqlite/insert/)