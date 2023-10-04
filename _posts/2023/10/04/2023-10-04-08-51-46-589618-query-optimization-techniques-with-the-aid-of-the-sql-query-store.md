---
layout: post
title: "Query optimization techniques with the aid of the SQL Query Store"
description: " "
date: 2023-10-04
tags: [introduction), enabling]
comments: true
share: true
---

## Introduction

The SQL Server Query Store is a powerful feature that comes with SQL Server 2016 and above. It assists database administrators and developers in analyzing and troubleshooting query performance by capturing query execution plans, metrics, and runtime statistics. In this blog post, we will explore some query optimization techniques using the SQL Query Store.

## Table of Contents
- [Introduction](#introduction)
- [Enabling the Query Store](#enabling-the-query-store)
- [Identifying Query Performance Issues](#identifying-query-performance-issues)
- [Forcing Query Plans](#forcing-query-plans)
- [Monitoring Query Plan Changes](#monitoring-query-plan-changes)
- [Identifying and Fixing Plan Regression](#identifying-and-fixing-plan-regression)
- [Summary](#summary)

## Enabling the Query Store

Before we can take advantage of the Query Store, it needs to be enabled on the database level. The following SQL script enables the Query Store on a database:

```sql
ALTER DATABASE [DatabaseName]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));
```

## Identifying Query Performance Issues

Once the Query Store is enabled, it starts capturing query execution information. To identify queries with performance issues, we can query the Query Store views to get insights into the top resource-consuming queries, high duration queries, or queries with poor execution plans.

Here's an example query that retrieves queries with high average duration:

```sql
SELECT TOP 10
    qt.query_text_id,
    qt.query_sql_text,
    qep.query_execution_plan_xml,
    rs.avg_duration
FROM
    sys.query_store_query q
    JOIN sys.query_store_query_text qt ON qt.query_text_id = q.query_text_id
    JOIN sys.query_store_plan p ON p.plan_id = q.plan_id
    JOIN sys.query_store_runtime_stats rs on rs.plan_id = p.plan_id
WHERE
    rs.avg_duration > 1000 -- Specify a threshold
ORDER BY
    rs.avg_duration DESC;
```

## Forcing Query Plans

In some cases, the SQL Server Query Optimizer may generate suboptimal execution plans, resulting in poor query performance. With the Query Store, we can force a specific execution plan for a problematic query.

To force a plan, execute the following SQL statement:

```sql
EXEC sp_query_store_force_plan <plan_id>;
```

## Monitoring Query Plan Changes

The Query Store helps track changes in query plans over time. By monitoring plan changes, we can identify query performance regression or plan instability issues.

To monitor plan changes, we can use the following query:

```sql
SELECT
    q.query_id,
    qt.query_sql_text,
    p.plan_id,
    p.is_forced_plan,
    p.last_compile_start_time
FROM
    sys.query_store_query q
    JOIN sys.query_store_query_text qt ON qt.query_text_id = q.query_text_id
    JOIN sys.query_store_plan p ON p.query_id = q.query_id
WHERE
    p.is_forced_plan = 0 -- Exclude forced plans
ORDER BY
    p.last_compile_start_time DESC;
```

## Identifying and Fixing Plan Regression

Plan regression occurs when a previously performing query suddenly starts performing poorly due to changes in the execution plan. The Query Store helps to identify and fix plan regression issues.

To identify plan regressions, we can use the following query:

```sql
SELECT
    q.query_id,
    qt.query_sql_text,
    p.plan_id,
    rs.*
FROM
    sys.query_store_query q
    JOIN sys.query_store_query_text qt ON qt.query_text_id = q.query_text_id
    JOIN sys.query_store_plan p ON p.query_id = q.query_id
    JOIN sys.query_store_runtime_stats rs ON rs.plan_id = p.plan_id
WHERE
    rs.avg_duration > 2 * rs.avg_duration_base AND
    rs.last_execution_time > DATEADD(HOUR, -1, GETUTCDATE()) -- Limit to recent data
ORDER BY
    rs.avg_duration DESC;
```

Once a plan regression is identified, we can force the previous plan that performed well using the `sp_query_store_force_plan` procedure discussed earlier.

## Summary

The SQL Server Query Store is a valuable tool for optimizing query performance. By enabling the Query Store, identifying query performance issues, forcing query plans, monitoring plan changes, and fixing plan regressions, we can significantly improve the performance of our SQL queries.