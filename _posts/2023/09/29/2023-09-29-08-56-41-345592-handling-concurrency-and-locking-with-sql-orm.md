---
layout: post
title: "Handling concurrency and locking with SQL ORM"
description: " "
date: 2023-09-29
tags: [concurrency, locking]
comments: true
share: true
---

In an application that interacts with a database using an **SQL ORM (Object-Relational Mapping)**, it is crucial to handle concurrency and locking properly to ensure data integrity and prevent race conditions. Concurrency refers to multiple users or processes accessing and modifying the same data simultaneously, while locking is the mechanism used to control access to shared resources.

## Optimistic Concurrency Control

One common approach to handle concurrency in SQL ORMs is **Optimistic Concurrency Control (OCC)**. This approach assumes that conflicts between concurrent transactions are rare and optimistic locking is used to detect conflicts rather than preventing them in advance. Here's how it typically works:

1. Each record in the database is associated with a version or timestamp column.
2. When a record is read, the version/timestamp value is fetched along with the record.
3. When an update is made, the database compares the version/timestamp value of the record being updated with the version/timestamp value stored in the database.
4. If the values match, the update is allowed, and the version/timestamp is incremented.
5. If the values don't match, it means that the record has been modified by another transaction, and an exception or error is raised to handle the conflict.

By using OCC, conflicts are handled after the update is attempted, which increases the system's performance but requires proper handling of conflicts to ensure data consistency.

## Pessimistic Locking

Alternatively, you can use **Pessimistic Locking** to prevent conflicts from occurring in the first place. In this approach, when a record is accessed, a lock is acquired on it until the transaction is completed. This prevents other transactions from modifying the locked record until the lock is released.

Pessimistic locking can be implemented using different types of locks, such as:

- **Shared Locks**: Allow multiple transactions to read a record but prevent any transaction from modifying it.
- **Exclusive Locks**: Ensure exclusive access to a record, preventing any other transactions from both reading and modifying it.

The choice of lock type depends on the specific requirements of your application.

## Example Code

Here's an example using an SQL ORM (specifically in Python using SQLAlchemy) to demonstrate handling concurrency and locking:

```python
from sqlalchemy import Column, Integer, String, DateTime
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
from sqlalchemy import update, select
from datetime import datetime

Base = declarative_base()


class Product(Base):
    __tablename__ = "products"

    id = Column(Integer, primary_key=True)
    name = Column(String)
    quantity = Column(Integer)
    last_updated = Column(DateTime)


# Example of optimistic concurrency control
def update_product(product_id, new_quantity):
    session = sessionmaker()
    record = session.query(Product).filter(Product.id == product_id).first()

    if record:
        if record.quantity < new_quantity:
            raise Exception("Insufficient quantity")

        record.quantity = new_quantity
        record.last_updated = datetime.now()

        session.commit()
    else:
        raise Exception("Product not found")


# Example of pessimistic locking
def get_product_quantity(product_id):
    session = sessionmaker()
    with session.begin():
        record = session.query(Product).with_for_update().filter(Product.id == product_id).first()

        if record:
            return record.quantity
        else:
            raise Exception("Product not found")


# Usage example
try:
    update_product(1, 10)
except:
    # Handle update conflict

try:
    quantity = get_product_quantity(1)
    print(quantity)
except:
    # Handle record retrieval conflict
```

In the code snippet above, we define a `Product` model using SQLAlchemy and provide examples of how to implement OCC and pessimistic locking. The methods `update_product` and `get_product_quantity` showcase how to handle conflicts when updating and retrieving records.

#concurrency #locking