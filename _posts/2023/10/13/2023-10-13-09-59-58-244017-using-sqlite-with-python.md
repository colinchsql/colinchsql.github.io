---
layout: post
title: "Using SQLite with Python"
description: " "
date: 2023-10-13
tags: []
comments: true
share: true
---

Python is a popular programming language that offers a wide range of libraries and modules for different purposes. One of the libraries commonly used for database management in Python is SQLite. SQLite is a lightweight and serverless database engine that can be easily integrated into Python applications.

In this blog post, we will explore how to use SQLite with Python and perform various database operations such as creating tables, inserting data, querying data, and updating records.

## Table of Contents
1. [Installing SQLite](#installing-sqlite)
2. [Connecting to SQLite in Python](#connecting-to-sqlite-in-python)
3. [Creating a Table](#creating-a-table)
4. [Inserting Data](#inserting-data)
5. [Querying Data](#querying-data)
6. [Updating Records](#updating-records)
7. [Conclusion](#conclusion)

## Installing SQLite
Before we begin, make sure you have SQLite installed on your system. If not, you can download SQLite from the official website (https://www.sqlite.org/download.html) and follow the installation instructions for your operating system.

## Connecting to SQLite in Python
To interact with an SQLite database in Python, we need to import the `sqlite3` module. This module provides the necessary functions and methods to connect to a SQLite database, execute SQL statements, and handle results.

```python
import sqlite3

# Connect to an existing SQLite database or create a new one
conn = sqlite3.connect('example.db')

# Create a cursor object to execute SQL statements
cursor = conn.cursor()

# Perform database operations...

# Close the database connection
conn.close()
```

## Creating a Table
To create a table in SQLite, we need to execute a CREATE TABLE statement. We can use the `execute()` method of the cursor object to execute SQL statements.

```python
# Create a table
cursor.execute('''CREATE TABLE employees
                  (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)''')
```

## Inserting Data
To insert data into an SQLite table, we need to execute an INSERT statement. We can use the `execute()` method with placeholders (`?`) to pass values dynamically.

```python
# Insert a single record
cursor.execute("INSERT INTO employees VALUES (?, ?, ?)", (1, 'John Doe', 25))

# Insert multiple records
employees = [
    (2, 'Jane Smith', 30),
    (3, 'Mike Johnson', 35)
]
cursor.executemany("INSERT INTO employees VALUES (?, ?, ?)", employees)
```

## Querying Data
To retrieve data from an SQLite table, we can execute a SELECT statement. We can use the `execute()` method to execute the query and fetch the results using the `fetchall()` method.

```python
# Select all records from the table
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()

# Iterate over the results
for row in rows:
    print(row)
```

## Updating Records
To update records in an SQLite table, we can execute an UPDATE statement. We can use the `execute()` method with placeholders (`?`) to pass the values dynamically.

```python
# Update a record
cursor.execute("UPDATE employees SET age = ? WHERE id = ?", (26, 1))
```

## Conclusion
In this blog post, we have explored how to use SQLite with Python. We learned how to connect to a SQLite database, create tables, insert data, query data, and update records. SQLite provides a lightweight and efficient way to handle databases in Python applications.