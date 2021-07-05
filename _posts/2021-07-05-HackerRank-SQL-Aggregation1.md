---
title : HackerRank-Aggregation-Revising Aggregations - The Count Function

tags:
    - sql
categories:
    - sql 
date: '2021-07-05'

---

# Revising Aggregations - The Count Function


Query a _count_ of the number of cities in **CITY** having a _Population_ larger than 100,000.

**Input Format**
The **CITY** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

**My solution**
```sql
SELECT COUNT(NAME)
FROM CITY
WHERE population > 100000;
```

![](https://i.imgur.com/Dd68AXE.png)


