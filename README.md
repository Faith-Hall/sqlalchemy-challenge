# sqlalchemy-challenge
---
### Part 1: Analyze and Explore the Climate Data
I did a climate analysis and exploration of the ```hawaii.sqlite``` file. 

- I found the most recent date in the dataset by querrying the maximum value from the measurement class in the date column.
```
most_recent_date_str = session.query(func.max(Measurement.date)).scalar()
```
- From here, I gathered the previous year of precipitation data by querying the previous 12 months of data.
```
start_date = most_recent_date - dt.timedelta(days = 365)
``` 
- Selected the date and prcp values
```
data = session.query(Measurement.date, func.avg(Measurement.prcp)).\
    filter(Measurement.date >= start_date).\
    group_by(Measurement.date).\
    all()
```
