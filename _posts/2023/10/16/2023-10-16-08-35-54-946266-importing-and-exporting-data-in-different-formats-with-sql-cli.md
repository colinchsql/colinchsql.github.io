---
layout: post
title: "Importing and exporting data in different formats with SQL CLI"
description: " "
date: 2023-10-16
tags: [data]
comments: true
share: true
---

In this blog post, we will explore how to import and export data in various formats using SQL command-line interface (CLI). SQL CLI provides a convenient way to interact with databases and perform data operations. We will focus on the common file formats such as CSV, JSON, and XML.

## Table of Contents
- [Importing Data](#importing-data)
    - [CSV](#csv)
    - [JSON](#json)
    - [XML](#xml)
- [Exporting Data](#exporting-data)
    - [CSV](#csv-1)
    - [JSON](#json-1)
    - [XML](#xml-1)
- [Conclusion](#conclusion)

## Importing Data

### CSV

To import data from a CSV file using SQL CLI, we can use the `COPY` command with the `FROM` keyword followed by the file path. Here's an example:

```sql
COPY my_table FROM '/path/to/data.csv' WITH (FORMAT CSV, HEADER);
```

The `FORMAT CSV` option specifies that the file format is CSV, and the `HEADER` option indicates that the first row of the CSV file contains column headers.

### JSON

To import data from a JSON file using SQL CLI, we can use the `COPY` command with the `FROM` keyword and specify the file path. Here's an example:

```sql
COPY my_table FROM '/path/to/data.json' WITH (FORMAT JSON);
```

The `FORMAT JSON` option tells SQL CLI to interpret the file content as JSON.

### XML

Importing data from an XML file using SQL CLI requires some additional steps. First, we need to create an external table that corresponds to the XML structure. Then, we can use the `COPY` command to import data from the XML file into the table.

```sql
-- Create external table
CREATE EXTERNAL TABLE my_table (col1 data_type, col2 data_type)
LOCATION '/path/to/external/table';

-- Import data from XML file
COPY my_table FROM '/path/to/data.xml' WITH (FORMAT XML);
```

The `CREATE EXTERNAL TABLE` command creates a table with the specified structure, and the `LOCATION` parameter is used to define the directory where the external table resides.

## Exporting Data

### CSV

To export data from a table to a CSV file using SQL CLI, we can use the `COPY` command with the `TO` keyword followed by the file path. Here's an example:

```sql
COPY my_table TO '/path/to/output.csv' WITH (FORMAT CSV, HEADER);
```

The `FORMAT CSV` option specifies the file format as CSV, and the `HEADER` option includes column headers in the exported file.

### JSON

To export data from a table to a JSON file using SQL CLI, we can use the `COPY` command with the `TO` keyword and specify the file path. Here's an example:

```sql
COPY my_table TO '/path/to/output.json' WITH (FORMAT JSON);
```

The `FORMAT JSON` option tells SQL CLI to export data in JSON format.

### XML

Exporting data from a table to an XML file using SQL CLI requires the installation of an additional module. The `pg_xml` module provides functions to generate XML output. Once installed, we can use the `COPY` command to export data. Here's an example:

```sql
-- Install pg_xml module
CREATE EXTENSION pg_xml;

-- Export data to XML file
COPY (SELECT row_to_xml(my_table, true, false) FROM my_table) TO '/path/to/output.xml';
```

The `CREATE EXTENSION` command is used to install the `pg_xml` module, and the `row_to_xml` function converts rows into XML format.

## Conclusion

SQL CLI offers a powerful way to import and export data in various formats. By utilizing the `COPY` command and specifying the appropriate format, we can easily transfer data between different systems and files. Whether it's CSV, JSON, or XML, SQL CLI provides the flexibility to work with different data formats seamlessly.

#hashtags: #SQL #data-import-export