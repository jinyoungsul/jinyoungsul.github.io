# Weather Observation Station 15

Query the  _Western Longitude_  (_LONG_W_) for the largest  _Northern Latitude_  (_LAT_N_) in  **STATION**  that is less than 137.2345 . Round your answer to 4 decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(LONG_W, 4)
FROM 
(   SELECT *
    FROM STATION
    WHERE LAT_N < 137.2345 
    ORDER BY LAT_N DESC
)
WHERE ROWNUM = 1;
```




