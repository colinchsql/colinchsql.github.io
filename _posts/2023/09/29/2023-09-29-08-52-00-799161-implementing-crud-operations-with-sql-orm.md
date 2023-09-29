---
layout: post
title: "Implementing CRUD operations with SQL ORM"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement CRUD (Create, Read, Update, Delete) operations with a SQL Object-Relational Mapping (ORM) framework. ORM allows us to interact with a database using programming language objects instead of raw SQL queries.

## What is ORM?

ORM is a technique that enables developers to work with a relational database using an object-oriented programming paradigm. It abstracts the underlying SQL database and provides an interface to perform common database operations.

## Choosing an ORM Framework

There are several popular ORM frameworks available for different programming languages such as SQLAlchemy for Python, Hibernate for Java, and Django ORM for Django framework. In this example, we will be using SQLAlchemy with Python.

## Setting up the Environment

To get started, we need to install the required dependencies. Run the following command to install SQLAlchemy:

```python
pip install SQLAlchemy
```

Once installed, we can now import SQLAlchemy in our Python script:

```python
import sqlalchemy
from sqlalchemy.orm import sessionmaker
```

## Creating a Model

A model represents a table in the database. We define a class that maps to a table and its attributes to columns in the table. For example, let's create a model for a "User" table:

```python
from sqlalchemy import Column, Integer, String

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)
```

## Performing CRUD Operations

### Creating a Record

To create a new user record, we first need to create a session:

```python
Session = sessionmaker(bind=engine)
session = Session()
```

Then, we can create and add a new user to the session:

```python
new_user = User(name="John Doe", email="john@example.com")
session.add(new_user)
session.commit()
```

### Reading Records

To query records from the database, we can use the `query()` method:

```python
users = session.query(User).all()
```

We can also use filters to retrieve specific records:

```python
user = session.query(User).filter(User.id == 1).first()
```

### Updating a Record

To update a record, we first need to retrieve it from the database:

```python
user = session.query(User).filter(User.id == 1).first()
```

Then, we can update its attributes and commit the changes:

```python
user.name = "Updated Name"
session.commit()
```

### Deleting a Record

To delete a record from the database, we first need to retrieve it:

```python
user = session.query(User).filter(User.id == 1).first()
```

Then, we can remove it from the session and commit the changes:

```python
session.delete(user)
session.commit()
```

## Conclusion

Using a SQL ORM framework like SQLAlchemy simplifies the implementation of CRUD operations. We can create models, perform database operations, and handle the mapping between objects and tables effortlessly. ORM frameworks not only improve productivity but also provide a more intuitive and maintainable way of interacting with databases.

#sql #orm