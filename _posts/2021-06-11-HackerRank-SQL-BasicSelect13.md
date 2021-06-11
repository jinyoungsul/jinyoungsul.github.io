---
title : HackerRank-BasicSelect-Weather Observation Station 8

tags:
    - sql
categories:
    - sql 
date: '2021-06-11'

---

# Weather Observation Station 8

Query the list of  _CITY_  names from  **STATION**  which have vowels (i.e.,  _a_,  _e_,  _i_,  _o_, and  _u_) as both their first  _and_  last characters. Your result cannot contain duplicates.

**Input Format**

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[AEIOUaeiou][a-zA-Z ]*[AEIOUaeiou]$');
```

![](https://i.imgur.com/3MQgUEh.png)

