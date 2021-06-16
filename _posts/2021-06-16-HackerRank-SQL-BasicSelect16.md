---
title : HackerRank-BasicSelect-Weather Observation Station 11

tags:
    - sql
categories:
    - sql 
date: '2021-06-16'

---

# Weather Observation Station 11

Query the list of  _CITY_  names from  **STATION**  that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

**Input Format**

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

- 방법1
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[^AEIOU]') or REGEXP_LIKE(CITY, '[^aeiou]$');
```
-  방법2
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[^AEIOU]|[^aeiou]$');
```

![](https://i.imgur.com/1dIWADD.png)

