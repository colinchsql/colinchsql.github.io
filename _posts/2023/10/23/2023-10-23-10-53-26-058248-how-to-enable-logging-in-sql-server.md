---
layout: post
title: "How to enable logging in SQL Server"
description: " "
date: 2023-10-23
tags: [sqlserver, logging]
comments: true
share: true
---

When it comes to troubleshooting and analyzing issues in SQL Server, enabling logging can greatly help in identifying and resolving problems. Logging allows you to capture different types of events and information happening within SQL Server, such as errors, warnings, and performance-related data. In this article, we'll explore the steps to enable logging in SQL Server.

## 1. Using SQL Server Management Studio (SSMS)

1. Open SQL Server Management Studio (SSMS) and connect to your SQL Server instance.
2. Right-click on your SQL Server instance in the Object Explorer and select **Properties**.
3. In the **Server Properties** dialog, navigate to the **Logging** tab.
4. Check the boxes for the types of logs you want to enable, such as the **Error log**, **Query Store log**, or **SQL Server Profiler log**.
5. Specify the maximum number of log files to retain and the maximum size for each log file.
6. Click **OK** to save the changes.

## 2. Using Transact-SQL Commands

You can also enable logging using Transact-SQL commands. Follow these steps:

1. Open SSMS and connect to your SQL Server instance.
2. Open a new query window.
3. Run the following command to enable the error log:

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure 'error log', 1;
RECONFIGURE;
```

4. Run the following command to enable other logs, such as the query store log:

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure 'query store' , 1;
RECONFIGURE;
```

5. After running the commands, restart the SQL Server service to apply the changes.

## 3. Using SQL Server Configuration Manager

Another way to enable logging is through SQL Server Configuration Manager. Here's how:

1. Open SQL Server Configuration Manager.
2. Expand **SQL Server Services**.
3. Right-click on your SQL Server instance and select **Properties**.
4. In the **Startup Parameters** section, add the following parameters for different types of logs:

   - For the error log: `-e "C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log\ERRORLOG"`
   - For the query store log: `-T2128 -e "C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log\QueryStoreErrors"`

   Note: Adjust the file path based on your SQL Server instance and version.

5. Click **OK** to save the changes.
6. Restart the SQL Server service to apply the configuration.

Enabling logging in SQL Server provides valuable information that can assist in troubleshooting issues, allowing you to identify and resolve problems effectively. By following the steps outlined above, you can enable different types of logs to capture the necessary data for analysis.

For more information, refer to the official Microsoft SQL Server documentation: [SQL Server Logging](https://docs.microsoft.com/en-us/sql/relational-databases/errors-events/logging?view=sql-server-ver15)

**#sqlserver #logging**