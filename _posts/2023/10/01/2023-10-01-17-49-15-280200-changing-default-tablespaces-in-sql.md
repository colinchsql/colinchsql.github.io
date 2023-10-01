---
layout: post
title: "Changing default tablespaces in SQL"
description: " "
date: 2023-10-01
tags: [Database, Tablespace]
comments: true
share: true
---

In a SQL database, a default tablespace is the designated storage area for newly created tables and indexes. By default, the system assigns a default tablespace to every user in the database. However, there are scenarios where you might need to change the default tablespace for a user or the entire database. In this article, we will explore how to change default tablespaces in SQL.

### 1. Changing Default Tablespace for a User

To change the default tablespace for a specific user in SQL, you can use the `ALTER USER` statement. Follow the steps below:

1. Connect to the database using a privileged user account with the necessary permissions.
    ```sql
    CONNECT system/password;
    ```

2. Execute the `ALTER USER` statement, specifying the username and the new default tablespace.
    ```sql
    ALTER USER username DEFAULT TABLESPACE new_tablespace;
    ```

Replace `username` with the name of the user whose default tablespace you want to change, and `new_tablespace` with the name of the desired tablespace.

3. Confirm the changes by querying the `DBA_USERS` view.
    ```sql
    SELECT username, default_tablespace FROM dba_users WHERE username = 'username';
    ```

### 2. Changing Default Tablespace for the Entire Database

To change the default tablespace for the entire database, you need to modify the database parameter `DEFAULT_TABLESPACE`. Follow the steps below:

1. Connect to the database using a privileged user account.
    ```sql
    CONNECT system/password;
    ```

2. Set the new default tablespace using the `ALTER SYSTEM` statement.
    ```sql
    ALTER SYSTEM SET DEFAULT_TABLESPACE = new_tablespace;
    ```

Replace `new_tablespace` with the name of the desired tablespace.

3. Restart the database for the changes to take effect.

### Conclusion

Changing the default tablespace in SQL can be useful in various scenarios, such as when you want to allocate data to different storage areas or optimize database performance. By following the steps provided in this article, you can easily change the default tablespace for a user or the entire database. Remember to choose the appropriate tablespace based on your requirements and ensure you have the necessary privileges before making any changes.

Please reach out to our support team if you have any further questions or need assistance.

#SQL #Database #Tablespace