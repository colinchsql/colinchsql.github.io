---
layout: post
title: "How to create a Snowflake schema in SQL"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In data warehousing, a snowflake schema is a logical arrangement of tables in a relational database that is designed for improved query performance and optimized storage. It is an extension of the star schema, where dimensions are further normalized into multiple, smaller tables.

In this tutorial, we will go through the steps to create a snowflake schema in SQL.

## Table Structure

To create a snowflake schema, we need to create multiple tables for dimensions and fact tables. Let's assume we have the following tables:

1. `dimension_country` - Contains information about countries.
   - `id` - Primary key
   - `name` - Country name

2. `dimension_product` - Contains information about products.
   - `id` - Primary key
   - `name` - Product name
   - `category` - Product category

3. `dimension_time` - Contains information about time periods.
   - `id` - Primary key
   - `date` - Date
   - `month` - Month of the year
   - `quarter` - Quarter of the year
   - `year` - Year

4. `fact_sales` - Contains information about sales.
   - `id` - Primary key
   - `product_id` - Foreign key to `dimension_product`
   - `country_id` - Foreign key to `dimension_country`
   - `time_id` - Foreign key to `dimension_time`
   - `quantity` - Quantity sold
   - `revenue` - Revenue generated

## Creating Snowflake Schema

Here are the steps to create a snowflake schema SQL:

1. Create dimension tables:

   ```sql
   CREATE TABLE dimension_country (
       id INT PRIMARY KEY,
       name VARCHAR(255)
   );
   
   CREATE TABLE dimension_product (
       id INT PRIMARY KEY,
       name VARCHAR(255),
       category VARCHAR(255)
   );
   
   CREATE TABLE dimension_time (
       id INT PRIMARY KEY,
       date DATE,
       month INT,
       quarter INT,
       year INT
   );
   ```

2. Create the fact table:

   ```sql
   CREATE TABLE fact_sales (
       id INT PRIMARY KEY,
       product_id INT,
       country_id INT,
       time_id INT,
       quantity INT,
       revenue FLOAT,
       FOREIGN KEY (product_id) REFERENCES dimension_product(id),
       FOREIGN KEY (country_id) REFERENCES dimension_country(id),
       FOREIGN KEY (time_id) REFERENCES dimension_time(id)
   );
   ```

3. Ensure the appropriate indexes and constraints are in place for efficient querying and data integrity.

And that's it! You have now created a snowflake schema in SQL.

Remember to populate the dimension tables with data, and then you can insert data into the fact table to start analyzing your data using the snowflake schema.

**#datawarehousing #sql**

By following these steps, you can effectively create a snowflake schema in SQL for your data warehousing needs. This schema provides a structured and optimized way to store and analyze data, improving performance and ease of use.