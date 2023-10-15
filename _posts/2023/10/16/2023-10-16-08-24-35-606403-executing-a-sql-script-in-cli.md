---
layout: post
title: "Executing a SQL script in CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

When working with a database, there may be times when you need to execute SQL scripts from the command line interface (CLI). This can be useful for various purposes, such as running a batch of SQL statements, automating database tasks, or deploying database changes.

In this blog post, we will explore how to execute a SQL script in the CLI using different database systems.

## MySQL

To execute a SQL script in the MySQL CLI, you can use the `mysql` command as follows:

```sql
mysql -u <username> -p <database_name> < <script_file.sql>
```
- `<username>`: The username to connect to the MySQL server.
- `<database_name>`: The name of the database where you want to execute the script.
- `<script_file.sql>`: The path to the SQL script file.

For example, to execute a script named "data.sql" on a database called "mydb" as the user "root", you would use the following command:

```sql
mysql -u root -p mydb < data.sql
```

## PostgreSQL

To execute a SQL script in the PostgreSQL CLI, you can use the `psql` command as follows:

```sql
psql -U <username> -d <database_name> -f <script_file.sql>
```
- `<username>`: The username to connect to the PostgreSQL server.
- `<database_name>`: The name of the database where you want to execute the script.
- `<script_file.sql>`: The path to the SQL script file.

For example, to execute a script named "data.sql" on a database called "mydb" as the user "postgres", you would use the following command:

```sql
psql -U postgres -d mydb -f data.sql
```

## SQL Server

To execute a SQL script in the SQL Server CLI, you can use the `sqlcmd` command as follows:

```sql
sqlcmd -S <server_name> -U <username> -P <password> -d <database_name> -i <script_file.sql>
```
- `<server_name>`: The name of the SQL Server instance.
- `<username>`: The username to connect to the SQL Server.
- `<password>`: The password for the specified username.
- `<database_name>`: The name of the database where you want to execute the script.
- `<script_file.sql>`: The path to the SQL script file.

For example, to execute a script named "data.sql" on a database called "mydb" on a server named "localhost" with the user "sa" and password "mypassword", you would use the following command:

```sql
sqlcmd -S localhost -U sa -P mypassword -d mydb -i data.sql
```

## Conclusion

Executing a SQL script in the CLI can be a convenient way to automate database tasks or perform batch operations. By using the appropriate commands for your database system, you can easily execute SQL scripts and interact with your databases from the command line.

Be sure to refer to the official documentation for your specific database system for more detailed information and options.

Happy scripting!

**References:**
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Microsoft SQL Server Documentation](https://docs.microsoft.com/en-us/sql/)