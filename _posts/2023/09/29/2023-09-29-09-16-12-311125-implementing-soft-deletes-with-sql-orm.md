---
layout: post
title: "Implementing soft deletes with SQL ORM"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

When working with a SQL database, it's common to implement *soft deletes*. Soft deletes allow you to mark a record as deleted without actually removing it from the database. This approach is useful, for example, when you want to retain audit trails, maintain data integrity, or facilitate data recovery.

In this blog post, we'll explore how to implement soft deletes using a SQL Object-Relational Mapping (ORM) framework.

## Setting up the database

First, let's set up the database schema. We'll assume there is a `users` table with the following structure:

```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(255) NOT NULL,
  deleted_at DATETIME DEFAULT NULL
);
```

The `deleted_at` column will store the soft delete timestamp.

## Configuring the ORM

The exact implementation steps might vary depending on the ORM framework you are using. For this example, we'll use SQLAlchemy, a popular Python ORM.

1. Import the necessary modules:
```python
from sqlalchemy import Column, DateTime, String
from sqlalchemy.ext.declarative import declarative_base
```

2. Create a base model class and define the `deleted_at` column:
```python
Base = declarative_base()

class BaseModel(Base):
    __abstract__ = True
    deleted_at = Column(DateTime, nullable=True)
```
By setting `__abstract__ = True`, we tell SQLAlchemy that the `BaseModel` should not be mapped to a separate table.

3. Define your model classes, inheriting from the `BaseModel`:
```python
class User(BaseModel):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    username = Column(String(255), nullable=False)
```

## Implementing the soft delete functionality

To perform a soft delete, we simply update the `deleted_at` column with the current timestamp:

```python
from datetime import datetime

def soft_delete(session, model):
    model.deleted_at = datetime.utcnow()
    session.commit()
```

To retrieve non-deleted records, we can add a filter to the query:

```python
def get_active_users(session):
    return session.query(User).filter(User.deleted_at.is_(None)).all()
```

## Conclusion

Implementing soft deletes with a SQL ORM is quite straightforward. By adding a `deleted_at` column and a few additional methods, you can easily mark records as deleted without permanently removing them from your database.

As a final tip, remember to consider adding indexes to improve the performance of queries involving soft deletes.

#SQL #ORM