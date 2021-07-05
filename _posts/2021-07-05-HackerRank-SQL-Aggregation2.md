---
title : HackerRank-Aggregation-Revising Aggregations - The Sum Function

tags:
    - sql
categories:
    - sql 
date: '2021-07-05'

---

# Revising Aggregations - The Sum Function


Query the total population of all cities in  **CITY**  where  _District_  is  **California**.

**Input Format**
The **CITY** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

**My solution**
```sql
SELECT SUM(population)
FROM CITY
WHERE DISTRICT = 'California';
```

![](https://i.imgur.com/m3VkDp7.png)


