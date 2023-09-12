# sqlalchemy-challenge
---
### Part 1: Analyze and Explore the Climate Data
I did a climate analysis and exploration of the ```hawaii.sqlite``` file. 

- I found the most recent date in the dataset by querrying the maximum value from the measurement class in the date column.
```
most_recent_date_str = session.query(func.max(Measurement.date)).scalar()
```

