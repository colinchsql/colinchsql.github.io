---
layout: post
title: "Working with SQL CLI on different platforms (Windows, macOS, Linux)"
description: " "
date: 2023-10-16
tags: [References]
comments: true
share: true
---

When working with databases, it is often necessary to interact with SQL through a command line interface (CLI). SQL CLI provides a streamlined way to execute SQL queries, manage databases, and perform other database operations from the command line. In this article, we will explore how to work with SQL CLI on different platforms including Windows, macOS, and Linux.

## Windows

### Microsoft SQL Server

On Windows, Microsoft SQL Server provides its own command line tool called `sqlcmd`. To use `sqlcmd`, you need to have Microsoft SQL Server installed on your machine. Here are the steps to use `sqlcmd`:

1. Open the Command Prompt or PowerShell on your Windows machine.
2. Enter the `sqlcmd` command followed by the necessary arguments such as server name, username, and password.

```sql
sqlcmd -S server_name -U username -P password -d database_name
```

### MySQL

For interacting with MySQL databases on Windows, you can use the MySQL Command Line Client (`mysql.exe`). Here's how to use it:

1. Open the Command Prompt or PowerShell on your Windows machine.
2. Enter the `mysql` command followed by the necessary arguments such as hostname, username, and password.

```sql
mysql -h hostname -u username -p
```

## macOS and Linux

### PostgreSQL

On macOS and Linux, PostgreSQL provides the `psql` command line tool for interacting with PostgreSQL databases. To use `psql`, follow these steps:

1. Open the Terminal on your macOS or Linux machine.
2. Enter the `psql` command followed by the necessary arguments such as hostname, username, password, and database name.

```sql
psql -h hostname -U username -W -d database_name
```

### SQLite

For working with SQLite databases on macOS and Linux, you can use the `sqlite3` command line tool. Here's how to use it:

1. Open the Terminal on your macOS or Linux machine.
2. Enter the `sqlite3` command followed by the database file path.

```sql
sqlite3 /path/to/database.db
```

## Conclusion

Working with SQL CLI on different platforms is essential for managing and querying databases efficiently. Whether you are using Microsoft SQL Server, MySQL, PostgreSQL, or SQLite, each platform provides its own command line tool tailored for that specific database system. By familiarizing yourself with these tools and their usage on different platforms, you can enhance your productivity and streamline your database operations.

#References
1. [Microsoft SQL Server - sqlcmd Command Line Utility](https://docs.microsoft.com/en-us/sql/tools/sqlcmd-utility?view=sql-server-ver15)
2. [MySQL Documentation - mysql Command-Line Tool](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-command-line-client.html)
3. [PostgreSQL Documentation - psql](https://www.postgresql.org/docs/current/app-psql.html)
4. [SQLite Documentation - Command Line Shell For SQLite](https://sqlite.org/cli.html)