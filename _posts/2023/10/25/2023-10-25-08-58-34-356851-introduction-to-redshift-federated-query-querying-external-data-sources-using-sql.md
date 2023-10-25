---
layout: post
title: "Introduction to Redshift federated query: querying external data sources using SQL."
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

Data is becoming increasingly distributed across multiple systems and platforms. As a result, it has become crucial for businesses to have the ability to access and query data from various sources seamlessly. Amazon Redshift, a powerful data warehouse solution, offers a feature called Federated Query that allows users to query and analyze data from external sources directly using SQL.

This blog post introduces you to Redshift Federated Query and explains how you can leverage this feature to query external data sources within your Redshift cluster.

## Table of Contents

- [What is Redshift Federated Query?](#what-is-redshift-federated-query)
- [Supported Data Sources](#supported-data-sources)
- [Setting Up a Federated Query](#setting-up-a-federated-query)
- [Writing Federated Queries](#writing-federated-queries)
- [Performance Considerations](#performance-considerations)
- [Conclusion](#conclusion)

## What is Redshift Federated Query?

Redshift Federated Query allows you to connect and query data stored in external data sources directly from your Redshift cluster. This feature essentially extends the reach of your Redshift queries to include data located in other databases, data lakes, or even SaaS applications. By leveraging the power of SQL, you can seamlessly integrate and analyze data from these external sources within your Redshift environment.

## Supported Data Sources

Redshift Federated Query supports a wide range of external data sources, including:

- Amazon RDS for PostgreSQL
- Amazon Aurora PostgreSQL
- Amazon RDS for MySQL
- Amazon Aurora MySQL
- Amazon RDS for MariaDB
- Amazon DocumentDB
- Amazon Athena
- Amazon EMR
- S3 data lakes

This extensive list of supported data sources ensures that you can access and query data from various systems, whether they are within the AWS ecosystem or external to it.

## Setting Up a Federated Query

To start using Redshift Federated Query, you need to set up and configure your Redshift cluster to establish connections with the external data sources. This involves creating and managing the necessary connection information, credentials, and configurations for each external data source.

Amazon provides detailed documentation on how to set up each specific data source connection within Redshift. You can find these instructions in the [official Redshift documentation](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-federated-query.html).

## Writing Federated Queries

Once you have set up the connections, you can start writing federated SQL queries in Redshift to access data from external sources. The process of writing federated queries is very similar to writing regular SQL queries within Redshift. You can use the same syntax, functions, and capabilities to manipulate and analyze data from both Redshift tables and external data sources.

Here's an example of a federated query that joins data from an external PostgreSQL database and a table within your Redshift cluster:

```sql
SELECT r.region_name, COUNT(c.customer_id) AS total_customers
FROM external_postgres.customers AS c
JOIN redshift.sales AS s ON c.customer_id = s.customer_id
JOIN redshift.regions AS r ON s.region_id = r.region_id
GROUP BY r.region_name
ORDER BY total_customers DESC;
```

In this example, the `external_postgres` schema refers to the connection to the PostgreSQL database, allowing you to access the `customers` table from that external source. By joining this table with the `sales` and `regions` tables within the Redshift cluster, you can perform a unified analysis of the data.

## Performance Considerations

When using Redshift Federated Query, it's important to consider the performance implications of querying external data sources. Since the data resides outside the Redshift cluster, network latency and resource availability can impact query execution times. It's recommended to optimize the performance of the external data sources and tune the federated query execution to achieve optimal results.

Additionally, caching query results and utilizing Redshift Spectrum, another feature of Redshift, can further enhance performance when working with federated queries. You can leverage Spectrum's ability to query data directly from S3 to offload some of the processing and reduce the amount of data transferred across the network.

## Conclusion

Redshift Federated Query brings the power of SQL to seamlessly access and analyze data from various external sources within your Redshift environment. By leveraging this feature, you can break down data silos and gain valuable insights from distributed data. Whether it's querying data lakes or connecting to your SaaS applications, Redshift Federated Query empowers you to harness the full potential of your data.

Start experimenting with Redshift Federated Query and explore the variety of external data sources it supports. Unlock the potential of your data by bringing it all together with Redshift.