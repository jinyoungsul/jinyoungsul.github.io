---
title : HackerRank-Aggregation-Weather Observation Station 19

tags:
    - sql
categories:
    - sql 
date: '2021-07-13'

---

# Weather Observation Station 19



Consider **P1(a,c)** and **P2(b,d)** to be two points on a 2D plane where **(a,b)** are the respective minimum and maximum values of  _Northern Latitude_  (_LAT_N_) and **(c,d)** are the respective minimum and maximum values of  _Western Longitude_  (_LONG_W_) in  **STATION**.

Query the  [Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance)  between points **P1** and  **P2** and  _format your answer_  to display **4** decimal digits.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(SQRT(POWER(MAX(LAT_N) - MIN(LAT_N),2) + POWER(MAX(LONG_W) - MIN(LONG_W),2)), 4)
FROM STATION;
```




