# sqlalchemy-challenge
---
### Part 1: Analyze and Explore the Climate Data

### Precipitation Analysis
---
I did a climate analysis and exploration of the ```hawaii.sqlite``` file. 

- Find the most recent date in the dataset
```
most_recent_date_str = session.query(func.max(Measurement.date)).scalar()
```
- Using that date, get the previous 12 months of precipitation data by querying the previous 12 months of data
```
start_date = most_recent_date - dt.timedelta(days = 365)
``` 
- Select only the "date" and "prcp" values. (I used the average of prcp to eliminate duplicate dates)
```
data = session.query(Measurement.date, func.avg(Measurement.prcp)).\
    filter(Measurement.date >= start_date).\
    group_by(Measurement.date).\
    all()
```
- Load the query results into a Pandas DataFrame. Explicitly set the column names.
```
precipitation = pd.DataFrame(data, columns=["date", "prcp"]).sort_values("date")
 ```
- Plot the results

![image](https://github.com/Faith-Hall/sqlalchemy-challenge/assets/135525815/e9b59d2d-3483-4a88-80ff-485c92475016)

- Print summary statistics
  
![image](https://github.com/Faith-Hall/sqlalchemy-challenge/assets/135525815/617ccd1e-8fe1-4320-8300-d53ee149d332)

### Station Analysis
