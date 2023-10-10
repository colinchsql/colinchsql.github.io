---
layout: post
title: "Common types of SQL injection attacks."
description: " "
date: 2023-10-10
tags: [cybersecurity, sqlinjection]
comments: true
share: true
---

SQL injection attacks are one of the most common and dangerous web application vulnerabilities. They occur when an attacker manipulates user input to inject malicious SQL code into a query, potentially gaining unauthorized access to the database. In this article, we'll explore some common types of SQL injection attacks.

## 1. Classic SQL Injection

Classic SQL injection occurs when an attacker injects malicious SQL code into a query through user input fields. For example, consider the following vulnerable code snippet:

{% include codeHeader.html %}
```sql
username = getRequestParameter("username");
password = getRequestParameter("password");
query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'";
```
In this case, an attacker can manipulate the "username" parameter to inject additional SQL code. For instance, they can enter `' OR '1'='1'` as the username, causing the query to become:
{% include codeHeader.html %}
```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = 'password';
```
This would return all rows in the "users" table, effectively bypassing the authentication mechanism.

## 2. Blind SQL Injection

Blind SQL injection occurs when an attacker can't directly see the output of the injected SQL code. Instead, they infer information from the application's response. For example, consider the following code snippet:

{% include codeHeader.html %}
```sql
query = "SELECT * FROM users WHERE id = " + id + "'";
```
If the query returns a specific response when the condition is true (e.g., "User found"), and a different response when the condition is false (e.g., "User not found"), an attacker can exploit this behavior to extract information. They can use boolean-based or time-based techniques to infer the database's content, structure, or even execute arbitrary commands.

## 3. Union-based SQL Injection

Union-based SQL injection uses the UNION operator to combine the result set of a manipulated query with the result set of an unrelated query. It allows an attacker to extract data from other tables or even execute arbitrary SQL statements. For example, consider the following vulnerable code snippet:

{% include codeHeader.html %}
```sql
id = getRequestParameter("id");
query = "SELECT * FROM users WHERE id = " + id;
```
An attacker can inject a UNION-based payload to combine the original query with a parallel query that returns desired information. For instance, by injecting `' UNION SELECT username, password FROM admin --`, the attacker can retrieve the usernames and passwords of the admin users.

## 4. Time-based Blind SQL Injection

Time-based blind SQL injection exploits the server's delay in processing the injected SQL code. An attacker can inject code that forces the server to sleep for a specified amount of time, indicating if the injected condition is true or false. For example:

{% include codeHeader.html %}
```sql
query = "SELECT * FROM users WHERE id = " + id + "' AND (SLEEP(5) > 0)";
```
If the server delays for 5 seconds when the injected condition is true, the attacker can infer information based on the response time.

## Conclusion

SQL injection attacks can have severe consequences, including data breaches, unauthorized access, and system compromise. By understanding the common types of SQL injection attacks, developers can implement preventive measures such as input validation, parameterized queries, and prepared statements. It is crucial to adhere to secure coding practices and regularly update and patch your application to mitigate these vulnerabilities.

#cybersecurity #sqlinjection