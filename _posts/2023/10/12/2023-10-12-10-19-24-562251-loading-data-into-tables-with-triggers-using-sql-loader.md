---
layout: post
title: "Loading data into tables with triggers using SQL Loader."
description: " "
date: 2023-10-12
tags: [sqlloader, triggers]
comments: true
share: true
---

When it comes to loading large amounts of data into tables, SQL Loader is a powerful tool in the Oracle database. It provides a fast and efficient way to load data from external files into database tables. However, in some cases, you might need to perform additional actions or validations on the data before it is inserted into the tables. This is where triggers come in handy.

Triggers in Oracle are special types of stored procedures that are automatically executed when specific events occur, such as inserting, updating, or deleting data in a table. You can use triggers in conjunction with SQL Loader to perform custom actions before or after the data is loaded.

## Creating a Trigger

To start, let's create a trigger that will be fired before each row is inserted into the table. In this example, we want to convert a text column to uppercase before it is loaded into the table.

```sql
CREATE OR REPLACE TRIGGER convert_to_uppercase
BEFORE INSERT ON my_table
FOR EACH ROW
BEGIN
  :NEW.name := UPPER(:NEW.name);
END;
```

In the above trigger, `convert_to_uppercase` is the name of the trigger, `BEFORE INSERT` specifies that the trigger should execute before inserting a row, and `FOR EACH ROW` indicates that the trigger should be executed for each individual row being inserted.

Inside the trigger body, we are using the `UPPER()` function to convert the `name` column to uppercase and assigning the result back to the `name` column of the new row being inserted.

## Using SQL Loader with Triggers

Now, let's see how we can utilize SQL Loader to load data into the table with the trigger applied.

First, create a control file (e.g. `my_control.ctl`) that specifies the structure of the input file and the target table. Additionally, we need to specify the `TRIGGERFILE` parameter to indicate the location of the trigger file.

```sql
LOAD DATA
INFILE 'my_data.csv'
INTO TABLE my_table
TRIGGERFILE 'my_trigger.sql'
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
(
  id,
  name
)
```

In the control file, we define the input file (`my_data.csv`) and specify the target table (`my_table`) where the data will be loaded. The `TRIGGERFILE` parameter specifies the location of the trigger file (`my_trigger.sql`).

Next, create the trigger file (e.g. `my_trigger.sql`) and include the SQL code for the trigger we created earlier.

```sql
CREATE OR REPLACE TRIGGER convert_to_uppercase
BEFORE INSERT ON my_table
FOR EACH ROW
BEGIN
  :NEW.name := UPPER(:NEW.name);
END;
```

After creating the control file and the trigger file, we can use the following SQL Loader command to load the data into the table, taking advantage of the trigger that we defined.

```bash
sqlldr userid=username/password control=my_control.ctl log=my_log.log
```

In the above command, replace `username` and `password` with your Oracle database credentials. The `control` parameter specifies the location of the control file, and the `log` parameter specifies the location where the log file will be generated.

That's it! With the use of triggers and SQL Loader, you can easily perform custom actions or validations on the data while loading it into tables. This combination provides flexibility and control over the data loading process, making it a powerful tool for data integration in Oracle databases.

#sqlloader #triggers