---
layout: post
title: "Implementing data audit trail with SQL ORM"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

In modern business applications, data integrity and the ability to track changes to important data is crucial. One way to achieve this is by implementing a data audit trail, which records every change made to the database and provides a historical view of the data.

In this blog post, we will explore how to implement a data audit trail using a SQL Object Relational Mapping (ORM) framework. We will use **SQLAlchemy**, a popular Python ORM, as an example.

## The Data Audit Trail Table

To create a data audit trail, we need to create a separate table in the database that will store the historical changes made to the main table. This table can have columns like `id`, `table_name`, `column_name`, `old_value`, `new_value`, `timestamp`, and `user_id`.

```python
from sqlalchemy import Column, String, Integer, DateTime

class DataAuditTrail(Base):
    __tablename__ = 'data_audit_trail'

    id = Column(Integer, primary_key=True)
    table_name = Column(String(255))
    column_name = Column(String(255))
    old_value = Column(String(255))
    new_value = Column(String(255))
    timestamp = Column(DateTime)
    user_id = Column(Integer)
```

## Intercepting ORM Events

The next step is to intercept the ORM events that correspond to database updates or inserts. In SQLAlchemy, we can use event listeners to capture these events and store the changes in the data audit trail table.

```python
from sqlalchemy import event

@event.listens_for(Model, 'before_update')
def before_update_listener(mapper, connection, target):
    for attr, value in target.__dict__.items():
        if value != mapper.original[attr]:
            # Create a new AuditTrail entry for each changed attribute
            audit_trail = DataAuditTrail(
                table_name=mapper.class_.__tablename__,
                column_name=attr,
                old_value=mapper.original[attr],
                new_value=value,
                timestamp=datetime.now(),
                user_id=current_user.id
            )
            connection.add(audit_trail)

@event.listens_for(Model, 'before_insert')
def before_insert_listener(mapper, connection, target):
    # Create a new AuditTrail entry for the inserted row
    audit_trail = DataAuditTrail(
        table_name=mapper.class_.__tablename__,
        column_name="new_row",
        old_value="",
        new_value=target.__dict__,
        timestamp=datetime.now(),
        user_id=current_user.id
    )
    connection.add(audit_trail)
```

## Querying the Data Audit Trail

Now that we have the data audit trail table populated with historical changes, we can query it to retrieve the change history for any record.

```python
# Get all changes for a specific table and record
changes = session.query(DataAuditTrail).filter_by(table_name='my_table', user_id=current_user.id).all()

# Iterate over the changes and display the details
for change in changes:
    print(f"Column '{change.column_name}' changed from '{change.old_value}' to '{change.new_value}' at {change.timestamp}")
```

## Conclusion

Implementing a data audit trail using a SQL ORM framework like SQLAlchemy allows us to easily track changes to important data in our applications. By creating a separate table to store the historical changes and intercepting ORM events, we can provide an audit trail for data integrity and compliance purposes.

#sql #orm