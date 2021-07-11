---
title : HackerRank-Aggregation-Weather Observation Station 15

tags:
    - sql
categories:
    - sql 
date: '2021-07-10'

---

# Weather Observation Station 16

Query the smallest  _Northern Latitude_  (_LAT_N_) from  **STATION**  that is greater than 38.7780 . Round your answer to 4 decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(MIN(LAT_N),4)
FROM STATION
WHERE LAT_N > 38.7780;
```




