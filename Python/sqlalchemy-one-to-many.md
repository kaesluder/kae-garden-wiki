# SQL Alchemy One-to-Many

Written for: [[https://github.com/kaesluder/task-list-api]]

One-to-many relationship.

### Parent

```python
class Goal(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    title = db.Column(db.String, nullable=False)

    # one to many

    tasks = db.relationship("Task", back_populates="goal")
```

### Child

```python
class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    title = db.Column(db.String, nullable=False)
    description = db.Column(db.String)
    completed_at = db.Column(db.DateTime)

    # many to one
    goal_id = db.Column(db.Integer, db.ForeignKey("goal.id"))
    goal = db.relationship("Goal", back_populates="tasks")

```