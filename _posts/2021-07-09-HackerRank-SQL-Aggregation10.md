# Weather Observation Station 2



Query the following two values from the  **STATION**  table:

1.  The sum of all values in  _LAT_N_  rounded to a scale of 2 decimal places.
2.  The sum of all values in  _LONG_W_  rounded to a scale of 2 decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(SUM(LAT_N),2 ), ROUND(SUM(LONG_W), 2)
FROM STATION;
```




