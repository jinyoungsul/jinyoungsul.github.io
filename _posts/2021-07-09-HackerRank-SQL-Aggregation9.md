---
title : HackerRank-Aggregation-Weather Observation Station 13

tags:
    - sql
categories:
    - sql 
date: '2021-07-09'

---

# Weather Observation Station 13


Query the sum of  _Northern Latitudes_  (_LAT_N_) from  **STATION**  having values greater than 38.7880 and less than 137.2345 . Truncate your answer to  decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT round(sum(LAT_N),4)
FROM STATION
WHERE LAT_N > 38.7880 and LAT_N < 137.2345;
```

![](https://i.imgur.com/R3tUSwL.png)


