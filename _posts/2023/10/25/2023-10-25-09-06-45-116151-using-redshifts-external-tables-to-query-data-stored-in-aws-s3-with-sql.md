---
layout: post
title: "Using Redshift's external tables to query data stored in AWS S3 with SQL."
description: " "
date: 2023-10-25
tags: [analytics]
comments: true
share: true
---

AWS Redshift's external tables feature allows you to query data stored in AWS S3 directly from your Redshift cluster using SQL. This provides a convenient and efficient way to access large amounts of data without having to load it into Redshift first. In this blog post, we'll walk through the steps of setting up and querying external tables in Redshift.

## Table of Contents
- [What are External Tables?](#what-are-external-tables)
- [Setting Up an External Table](#setting-up-an-external-table)
- [Querying Data from External Tables](#querying-data-from-external-tables)
- [Performance Considerations](#performance-considerations)
- [Conclusion](#conclusion)
- [References](#references)

## What are External Tables?
**External tables** in Redshift are virtual tables that reference data files stored in AWS S3. These tables do not physically store the data within Redshift, but instead provide a schema and metadata for the files in S3. This allows you to query the data in S3 using standard SQL statements.

## Setting Up an External Table
To set up an external table in Redshift, you'll need to perform the following steps:

1. **Create an IAM Role**: Create an IAM role with the necessary permissions to access the S3 bucket where your data is stored. This role will be used by Redshift to access the S3 files.

2. **Create a Redshift Database**: Create a Redshift database where you'll create the external table. This can be done through the AWS Management Console or by using the AWS CLI.

3. **Create an External Schema**: Create an external schema within the Redshift database. This schema will be used to organize the external tables. You can create the schema using the `CREATE EXTERNAL SCHEMA` SQL statement.

4. **Create the External Table**: Use the `CREATE EXTERNAL TABLE` SQL statement to create the external table. Specify the S3 path where your data is stored, the IAM role to use, and the table schema. You can also define column mappings, data formats, and compression options.

5. **Verify the External Table**: Run a `SELECT` query on the external table to verify that it is correctly set up and you can access the data stored in S3.

## Querying Data from External Tables
Once the external table is set up, you can query the data using standard SQL statements. You can use the table in joins with other internal tables, apply filters, aggregations, and perform any other SQL operations supported by Redshift.

For example, to query data from an external table named `my_external_table`, you can use the following SQL statement:

```sql
SELECT * FROM my_external_table WHERE category = 'electronics';
```

By executing this query, Redshift will read the data from S3 and return the results as if they were stored in a regular Redshift table.

## Performance Considerations
When working with external tables in Redshift, there are some performance considerations to keep in mind:

- **Data Localization**: Redshift will attempt to move as much data as possible from S3 into the local disk of the cluster's compute nodes to improve query performance. However, it's still important to optimize your queries and table design to minimize data movement overhead.

- **Data Formats and Compression**: Choosing the right data format and compression options for your external table can greatly impact query performance. For example, using columnar compression formats like Parquet or ORC can help reduce storage footprint and improve query speed.

- **Partitioning**: If your data in S3 is partitioned, you can take advantage of partition pruning in Redshift by defining the partitioning scheme in the external table. This can significantly improve query performance by minimizing the amount of data scanned.

- **Maintenance and Monitoring**: Regularly monitor the performance of your external tables and optimize them as needed. This may include data reorganization, vacuuming, or updating statistics.

## Conclusion
Using external tables in Redshift provides a powerful way to query and analyze your data stored in AWS S3 directly. By leveraging the scalability and performance benefits of Redshift, you can perform complex analytics on large datasets without the need to load the data into Redshift first.

In this blog post, we covered the basics of setting up and querying external tables in Redshift. By following the outlined steps and considering the performance considerations, you can make the most out of this feature and unlock the full potential of your data analysis in Redshift.

## References
- [Amazon Redshift External Tables Documentation](https://docs.aws.amazon.com/redshift/latest/dg/c-using-spectrum.html)
- [Effective Data Loading Into Amazon Redshift: Techniques and Best Practices](https://aws.amazon.com/blogs/big-data/ingest-data-amazon-redshift-best-practices/)
#analytics #aws