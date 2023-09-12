# sqlalchemy-challenge
---
### Part 1: Analyze and Explore the Climate Data

### Precipitation Analysis
---
I did a climate analysis and exploration of the ```hawaii.sqlite``` file. 

- I found the most recent date in the dataset by querrying the maximum value from the measurement class in the date column.
```
most_recent_date_str = session.query(func.max(Measurement.date)).scalar()
```
- From here, I gathered the previous year of precipitation data by querying the previous 12 months of data.
```
start_date = most_recent_date - dt.timedelta(days = 365)
``` 
- Selected the date and prcp values. (I used the average of prcp to eliminate duplicate dates)
```
data = session.query(Measurement.date, func.avg(Measurement.prcp)).\
    filter(Measurement.date >= start_date).\
    group_by(Measurement.date).\
    all()
```
- Saved query results to a Pandas DataFrame
```
precipitation = pd.DataFrame(data, columns=["date", "prcp"]).sort_values("date")
 ```
- Plotted the results

![image](https://github.com/Faith-Hall/sqlalchemy-challenge/assets/135525815/e9b59d2d-3483-4a88-80ff-485c92475016)

- Printed summary statistics
  
![image](https://github.com/Faith-Hall/sqlalchemy-challenge/assets/135525815/617ccd1e-8fe1-4320-8300-d53ee149d332)

### Station Analysis
