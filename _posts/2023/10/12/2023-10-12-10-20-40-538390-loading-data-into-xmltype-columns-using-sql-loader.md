---
layout: post
title: "Loading data into XMLType columns using SQL Loader."
description: " "
date: 2023-10-12
tags: []
comments: true
share: true
---

In Oracle database, XMLType is a datatype that allows you to store XML data in a structured manner. When working with large amounts of XML data, it is often more efficient to use SQL Loader for loading the data into XMLType columns rather than using traditional SQL INSERT statements.

## Prerequisites
Before you begin, make sure you have the following:

- Oracle database installed and running.
- SQL Loader utility installed and configured.
- A table with an XMLType column defined in your database.

## Step 1: Create a control file
The control file instructs SQL Loader on how to interpret the data in the input file and how to load it into the database. Create a control file (e.g., `xml_loader.ctl`) with the following content:

```sql
LOAD DATA
INFILE 'input.xml'
APPEND INTO TABLE xml_table
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
(xml_column CHAR)
```

In this example, we assume that the input data is in a CSV format and the XML data is enclosed in double quotes. Adjust the `TERMINATED BY` and `ENCLOSED BY` clauses according to your specific input file format.

## Step 2: Prepare the input file
Create an input file (e.g., `input.xml`) containing the XML data you want to load into the XMLType column. Each line in the file should contain a single XML document, enclosed in double quotes if necessary.

```text
"<book><title>Oracle Database Administration</title><author>John Doe</author></book>"
"<book><title>Introduction to SQL</title><author>Jane Smith</author></book>"
```

## Step 3: Run SQL Loader
Open a terminal or command prompt and navigate to the directory where the control file and input file are located. Run the following command to load the XML data into the XMLType column:

```shell
sqlldr username/password control=xml_loader.ctl
```

Replace `username` and `password` with your Oracle database credentials.

SQL Loader will parse the input file according to the control file specifications and load the data into the specified XMLType column in the target table.

## Conclusion
By using SQL Loader to load XML data into XMLType columns, you can efficiently handle large volumes of XML data in Oracle databases. This method is especially useful when dealing with data from external sources or migrating data from other systems.