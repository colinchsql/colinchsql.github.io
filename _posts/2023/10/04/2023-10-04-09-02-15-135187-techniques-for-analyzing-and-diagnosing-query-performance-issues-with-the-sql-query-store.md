---
layout: post
title: "Techniques for analyzing and diagnosing query performance issues with the SQL Query Store"
description: " "
date: 2023-10-04
tags: [enabling, query]
comments: true
share: true
---

![SQL Query Store](https://www.example.com/images/sql-query-store.png)

The SQL Query Store is a powerful feature in Microsoft SQL Server that helps you analyze and diagnose query performance issues. It tracks and stores query execution plans, runtime statistics, and other useful information for queries that run on your server. In this blog post, we will explore some techniques you can use to analyze and diagnose query performance issues using the SQL Query Store.

## Table of Contents
- [Enabling the Query Store](#enabling-the-query-store)
- [Query Performance Dashboard](#query-performance-dashboard)
- [Identifying Top Resource Consumers](#identifying-top-resource-consumers)
- [Comparing Query Performance](#comparing-query-performance)
- [Forcing Query Performance Plan](#forcing-query-performance-plan)
- [Conclusion](#conclusion)

## Enabling the Query Store

Before you can start analyzing query performance issues, you need to enable the Query Store on your SQL Server instance. To do this, you can run the following T-SQL statement:

```sql
ALTER DATABASE [YourDatabaseName] SET QUERY_STORE = ON;
```

Once the Query Store is enabled, it will start collecting data about query executions automatically.

## Query Performance Dashboard

The Query Performance Dashboard is a built-in tool in SQL Server Management Studio (SSMS) that provides a graphical representation of query performance metrics. To access the Query Performance Dashboard, right-click on your database in SSMS, select "Reports," and then choose "Standard Reports" > "Performance" > "Query Performance."

The Query Performance Dashboard displays information such as top resource-consuming queries, query execution times, average CPU time, and much more. It allows you to quickly identify queries that are causing performance bottlenecks.

## Identifying Top Resource Consumers

To identify the top resource-consuming queries, you can use the following T-SQL query:

```sql
SELECT TOP 10 
    [rs].[query_id],
    [qt].[text] AS [sql_text],
    [rs].[avg_duration],
    [rs].[avg_cpu_time],
    [rs].[avg_logical_io_reads],
    [rs].[avg_logical_io_writes],
    [rs].[execution_count]
FROM 
    [sys].[query_store_query] AS [qs]
    JOIN [sys].[query_store_query_text] AS [qt]
        ON [qs].[query_text_id] = [qt].[query_text_id]
    JOIN [sys].[query_store_runtime_stats] AS [rs]
        ON [qs].[query_id] = [rs].[query_id]
ORDER BY 
    [rs].[avg_duration] DESC;
```

This query will return the top 10 resource-consuming queries, along with metrics such as average duration, CPU time, logical IO reads, logical IO writes, and execution count.

## Comparing Query Performance

The Query Store allows you to compare the performance of different query versions, which can be useful when analyzing performance variations after a code change or index optimization. You can use the following T-SQL query to compare the performance of two query versions:

```sql
SELECT 
    [qsv1].[query_id],
    [qt].[text] AS [sql_text],
    [qsv1].[avg_duration] AS [old_avg_duration],
    [qsv2].[avg_duration] AS [new_avg_duration]
FROM 
    [sys].[query_store_query] AS [qs]
    JOIN [sys].[query_store_query_text] AS [qt]
        ON [qs].[query_text_id] = [qt].[query_text_id]
    JOIN [sys].[query_store_plan] AS [qsp1]
        ON [qs].[query_id] = [qsp1].[query_id]
    JOIN [sys].[query_store_plan] AS [qsp2]
        ON [qs].[query_id] = [qsp2].[query_id]
    JOIN [sys].[query_store_runtime_stats] AS [qsv1]
        ON [qs].[query_id] = [qsv1].[query_id] 
        AND [qsp1].[plan_id] = [qsv1].[plan_id]
    JOIN [sys].[query_store_runtime_stats] AS [qsv2]
        ON [qs].[query_id] = [qsv2].[query_id] 
        AND [qsp2].[plan_id] = [qsv2].[plan_id]
WHERE
    [qsp1].[create_time] < [qsp2].[create_time]
```

This query will return the average duration for two query versions, allowing you to compare their performance.

## Forcing Query Performance Plan

In some cases, you might notice that a query is not using the optimal execution plan, resulting in poor performance. The Query Store allows you to force a specific execution plan for a query. You can use the following T-SQL statement to force a performance plan:

```sql
EXEC sp_query_store_force_plan 
    @query_id = [YourQueryID],
    @plan_id = [YourPlanID];
```

Make sure to replace `[YourQueryID]` and `[YourPlanID]` with the actual query and plan IDs.

## Conclusion

The SQL Query Store is a valuable tool for analyzing and diagnosing query performance issues. By enabling the Query Store and utilizing its features such as the Query Performance Dashboard, identifying top resource consumers, comparing query performance, and forcing query performance plans, you can effectively troubleshoot and optimize your SQL queries for better performance.

#seo #querystore #sql+#performance