---
layout: post
title: "Optimizing ad-hoc and parameterized queries using the SQL Query Store"
description: " "
date: 2023-10-04
tags: [understanding, optimizing]
comments: true
share: true
---

The SQL Query Store is a powerful feature in Microsoft SQL Server that allows you to monitor and optimize query performance. It helps identify and troubleshoot poorly performing queries by storing a history of query plans and runtime statistics. In this blog post, we will explore how to leverage the SQL Query Store to optimize ad-hoc and parameterized queries.

## Table of Contents
- [Understanding the SQL Query Store](#understanding-the-sql-query-store)
- [Optimizing Ad-hoc Queries](#optimizing-ad-hoc-queries)
- [Optimizing Parameterized Queries](#optimizing-parameterized-queries)
- [Monitoring Query Performance](#monitoring-query-performance)
- [Conclusion](#conclusion)

## Understanding the SQL Query Store

The SQL Query Store captures and retains query execution plans and runtime statistics for a specific database. It provides detailed insights into query performance over time, allowing you to identify and address performance bottlenecks.

To enable the Query Store for a database, use the following command:

```sql
ALTER DATABASE [DatabaseName] SET QUERY_STORE = ON;
```

Once enabled, you can configure various settings to control the amount of data stored, including retention period and maximum storage size.

## Optimizing Ad-hoc Queries

Ad-hoc queries are SQL statements that are not parameterized, meaning they are not compiled and cached for reuse. These queries pose a performance challenge, as each execution results in plan generation overhead, even if the query is executed multiple times.

By leveraging the SQL Query Store, you can identify the most frequently executed ad-hoc queries and their associated execution plans. This information allows you to identify performance issues, such as high CPU or excessive I/O, and optimize the queries accordingly.

To view ad-hoc queries captured by the Query Store, use the following query:

```sql
SELECT *
FROM sys.query_store_query q
WHERE q.query_type = 'Adhoc';
```

Once you have identified the problematic ad-hoc queries, you can use techniques such as query rewriting, adding indexes, or optimizing the query logic to improve their performance.

## Optimizing Parameterized Queries

Parameterized queries are SQL statements that use parameters instead of hard-coded values. They offer performance benefits by allowing the reuse of query plans. However, parameter sniffing can still cause suboptimal plans to be used for certain parameter values.

With the SQL Query Store, you can analyze the execution plans and runtime statistics of parameterized queries to identify cases where suboptimal plans are being used. You can then force the use of a specific plan, known as plan forcing, or update statistics to generate more accurate plans.

To identify parameterized queries captured by the Query Store, use the following query:

```sql
SELECT *
FROM sys.query_store_query q
WHERE q.query_type = 'Parameterized';
```

By analyzing the captured data, you can optimize the parameterized queries by applying techniques such as indexing, recompiling, or using the "OPTIMIZE FOR" query hint.

## Monitoring Query Performance

The SQL Query Store provides several built-in reports and dynamic management views (DMVs) to monitor query performance. These reports help identify top resource-consuming queries, query regressions, and other performance-related issues.

Some useful DMVs for monitoring query performance include:

- sys.query_store_runtime_stats
- sys.query_store_plan
- sys.query_store_query

You can also use the built-in reports, such as the "Top Resource Consuming Queries" report, to get a graphical representation of query performance metrics.

## Conclusion

The SQL Query Store is a valuable tool for optimizing ad-hoc and parameterized queries. By leveraging its features, you can easily identify poorly performing queries and take appropriate steps to improve their performance. By optimizing queries, you can enhance overall database performance and provide a better user experience.

#hashtags: #SQLQueryStore #QueryOptimization