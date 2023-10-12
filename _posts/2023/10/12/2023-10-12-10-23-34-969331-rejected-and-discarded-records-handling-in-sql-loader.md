---
layout: post
title: "Rejected and discarded records handling in SQL Loader."
description: " "
date: 2023-10-12
tags: [SQLLoader, DataLoad]
comments: true
share: true
---

When loading data into an Oracle database using SQL Loader, it's essential to have a mechanism in place to handle rejected and discarded records. Rejected records are those that fail to meet the specified format or data constraints, while discarded records are those intentionally excluded from the loading process.

In this blog post, we'll explore how to handle rejected and discarded records effectively in SQL Loader, ensuring data integrity and preventing the loading process from being disrupted.

## Table of Contents
1. [Handling Rejected Records](#handling-rejected-records)
2. [Handling Discarded Records](#handling-discarded-records)
3. [Conclusion](#conclusion)

## Handling Rejected Records

SQL Loader provides a way to capture and handle rejected records separately. Rejected records can be redirected to an error file for further analysis and debugging. Follow the steps below to configure the handling of rejected records:

1. Add the `ERRORS` clause to the SQL Loader control file:
    ```sql
    INTO TABLE tablename
    ...
    ...
    ERRORS <error_count>
    ```
   The `<error_count>` parameter specifies the maximum number of errors allowed before the loading process is terminated.

2. Specify the error file name using the `LOG` keyword:
    ```sql
    INTO TABLE tablename
    ...
    ...
    ERRORS <error_count>
    LOG '<error_file_name>.bad'
    ```

3. Any records that fail during the loading process will be written to the error file specified in the control file. Analyze this file to understand the causes of the rejection and make the necessary corrections.

By redirecting rejected records to an error file, we can thoroughly investigate and resolve the issues causing the rejections before reattempting the data load.

## Handling Discarded Records

Discarded records refer to those that are intentionally excluded from the loading process. For example, you may have specific conditions in your control file that determine which records to include or exclude.

To handle discarded records in SQL Loader, follow these steps:

1. Specify the relevant conditions in your control file for excluding records. For example:
    ```sql
    INTO TABLE tablename
    ...
    ...
    WHEN (1:3) <> 'ABC'
    ```

2. The records that match the exclusion conditions will be discarded and not loaded into the target table.

3. You can optionally redirect discarded records to a discard file using the `DISCARDFILE` keyword in the control file:
    ```sql
    DISCARDFILE '<discard_file_name>.dsc'
    ```

4. Analyze the discard file to ensure the correct records were discarded as per your conditions. Make any necessary adjustments to the control file if required.

Using the discard file, you can validate that the discarded records meet your exclusion criteria, maintaining data accuracy during the loading process.

## Conclusion

Handling rejected and discarded records is crucial while loading data into an Oracle database using SQL Loader. By configuring the appropriate options in the control file, you can redirect rejected records to an error file for analysis and debugging, and discard records that meet certain exclusion conditions. This ensures data integrity and prevents disrupting the loading process.

By utilizing SQL Loader's rejected and discarded records handling features, you can efficiently load data while maintaining data accuracy and integrity.

## #SQLLoader #DataLoad