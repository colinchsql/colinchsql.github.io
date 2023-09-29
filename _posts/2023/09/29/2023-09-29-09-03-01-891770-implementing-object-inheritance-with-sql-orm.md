---
layout: post
title: "Implementing object inheritance with SQL ORM"
description: " "
date: 2023-09-29
tags: [Inheritance]
comments: true
share: true
---

In this blog post, we will explore how to implement object inheritance using an SQL ORM, focusing on two common approaches: table-per-class hierarchy and table-per-concrete-class.

## Table-per-Class Hierarchy

In this approach, each class in the inheritance hierarchy maps to its own table in the database. The superclass and subclasses share a common primary key, with additional columns for subclass-specific attributes. Let's see an example using SQLAlchemy, a popular SQL ORM for Python:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Animal(Base):
    __tablename__ = 'animals'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    type = Column(String)
    __mapper_args__ = {'polymorphic_identity': 'animal', 'polymorphic_on': type}

class Dog(Animal):
    __tablename__ = 'dogs'
    id = Column(Integer, primary_key=True)
    breed = Column(String)
    __mapper_args__ = {'polymorphic_identity': 'dog'}

class Cat(Animal):
    __tablename__ = 'cats'
    id = Column(Integer, primary_key=True)
    color = Column(String)
    __mapper_args__ = {'polymorphic_identity': 'cat'}
```

In this example, the `Animal` class serves as the superclass, while `Dog` and `Cat` are the subclasses. Each class has its own table, with additional attributes specific to the subclass. The `__mapper_args__` attribute specifies the polymorphic identity to differentiate the objects.

## Table-per-Concrete-Class

In this approach, each class in the inheritance hierarchy maps to its own separate table, without a shared primary key. Each subclass table contains all the attributes from its superclass table, along with its specific attributes. Let's modify our previous example to demonstrate this approach:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Animal(Base):
    __tablename__ = 'animals'
    id = Column(Integer, primary_key=True)
    name = Column(String)

class Dog(Base):
    __tablename__ = 'dogs'
    id = Column(Integer, primary_key=True)
    breed = Column(String)
    name = Column(String)

class Cat(Base):
    __tablename__ = 'cats'
    id = Column(Integer, primary_key=True)
    color = Column(String)
    name = Column(String)
```

In this modified example, each class is mapped to its own table, with all attributes duplicated across the tables. This approach avoids the need for joins but can result in duplicate data.

Implementing object inheritance with an SQL ORM brings flexibility and structure to our database schema. The choice between table-per-class hierarchy and table-per-concrete-class depends on our specific use case and performance requirements.

#SQL #ORM #Inheritance