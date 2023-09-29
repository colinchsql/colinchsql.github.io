---
layout: post
title: "Mapping objects to databases using SQL ORM"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

In modern software development, Object Relational Mapping (ORM) has become a popular technique for mapping objects to databases. ORM allows developers to work with objects in their programming language of choice while abstracting away the complexities of interacting with a database.

One of the most widely used ORM frameworks is SQLAlchemy, which provides a powerful and flexible toolkit for working with relational databases using Python. Let's explore how SQLAlchemy enables developers to map and interact with database tables as objects.

## Declaring Database Tables as Python Classes ##

With SQLAlchemy, database tables are declared as Python classes, representing the structure and relationships of the data. Each class is a subclass of the `Base` class provided by SQLAlchemy, which handles the mapping between the Python objects and the database schema.

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)
```

In the above example, we define a simple `User` class with three attributes: `id`, `name`, and `email`. The `__tablename__` attribute specifies the name of the database table associated with this class.

## CRUD Operations with SQLAlchemy ##

Once the database tables are defined as Python classes, SQLAlchemy provides a set of powerful APIs to perform CRUD (Create, Read, Update, Delete) operations.

### Creating Objects ###

To create a new record in the `users` table, we can simply instantiate a `User` object and add it to the session:

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

engine = create_engine('sqlite:///mydatabase.db')
Session = sessionmaker(bind=engine)
session = Session()

new_user = User(name='John Doe', email='johndoe@example.com')
session.add(new_user)
session.commit()
```

### Querying Objects ###

To fetch data from the `users` table, SQLAlchemy provides a convenient querying interface:

```python
# Fetch all users
users = session.query(User).all()

# Fetch users with a specific name
specific_users = session.query(User).filter(User.name == 'John Doe'). all()
```

### Updating Objects ###

To update an existing record, we can modify the corresponding object and commit the changes:

```python
user = session.query(User).filter(User.name == 'John Doe').first()
user.email = 'newemail@example.com'
session.commit()
```

### Deleting Objects ###

To delete a record, we can simply remove it from the session and commit the changes:

```python
user = session.query(User).filter(User.name == 'John Doe').first()
session.delete(user)
session.commit()
```

## Conclusion ##

Using an ORM like SQLAlchemy simplifies the process of mapping objects to databases and performing CRUD operations. By defining classes that represent database tables and leveraging the provided APIs, developers can focus on writing Python code without worrying about the intricacies of SQL.

#sql #orm