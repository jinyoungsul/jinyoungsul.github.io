---
title : HackerRank-BasicSelect-Weather Observation Station 9

tags:
    - sql
categories:
    - sql 
date: '2021-06-12'

---

# Weather Observation Station 9


Query the list of  _CITY_  names from  **STATION**  that  _do not start_  with vowels. Your result cannot contain duplicates.

**Input Format**

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[^AEIOU]');
```

![](https://i.imgur.com/JYGvChY.png)

