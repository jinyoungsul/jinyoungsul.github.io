---
title : HackerRank-Aggregation-Weather Observation Station 20

tags:
    - sql
categories:
    - sql 
date: '2021-07-13'

---

# Weather Observation Station 20




A  _[median](https://en.wikipedia.org/wiki/Median)_  is defined as a number separating the higher half of a data set from the lower half. Query the  _median_  of the  _Northern Latitudes_  (_LAT_N_) from  **STATION**  and round your answer to 4 decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(LAT_N,4)
FROM
(
SELECT ROW_NUMBER() OVER(ORDER BY LAT_N asc) AS NUM,LAT_N
FROM STATION
)
WHERE NUM=(SELECT ROUND(COUNT(*) / 2)
           FROM STATION
          );
```




